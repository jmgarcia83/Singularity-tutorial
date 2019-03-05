# MPI
One of the architecturally defined features in Singularity is that it can execute containers like they are native programs or scripts on a host computer. As a result, integration with schedulers is simple and runs exactly as you would expect. All standard input, output, error, pipes, IPC, and other communication pathways that locally running programs employ are synchronized with the applications running locally within the container.

Additionally, because Singularity is not emulating a full hardware level virtualization paradigm, there is no need to separate out any sandboxed networks or file systems because there is no concept of user-escalation within a container. Users can run Singularity containers just as they run any other program on the HPC resource.

Include the appropriate development tools into the container (notice we are calling
singularity as root and the container is writable)

```
$ sudo singularity build --sandbox centos-7 library://centos:7
$ sudo singularity exec -w centos-7.sif yum groupinstall -y "Development Tools"
```
### Obtain the stable version of Open MPI
```
$ wget https://www.open-mpi.org/software/ompi/v2.1/downloads/openmpi-2.1.0.tar.bz2
$ tar -xf openmpi-2.1.0.tar.bz2
$ cd openmpi-2.1.0
$ singularity exec ../centos-7 ./configure --prefix=/usr/local
$ singularity exec ../centos-7 make -j$(nrpoc)
```
### Install OpenMPI into the container

> notice now running as root and container is writable

```
$ sudo singularity exec -w -B /home ../centos-7 make install
```
### Build the OpenMPI ring example and place the binary in this directory
```
$ singularity exec centos-7 mpicc openmpi-4.0.0/examples/ring_c.c -o ring

$ sudo singularity exec -w -B /home centos-7 cp ring /usr/bin/ring
```

Now that our sandbox has all the requirements to run mpi, let's save it as a SIF file

```
$ cd ..

$ sudo singularity build centos7.sif centos-7
```

### Run the MPI program within the container by calling the MPIRUN on the host

> *WARNING* MPI must be pre installed on the host

```
$ mpirun -np 4 singularity exec centos-7.sif /usr/bin/ring
```
### Submit mpi example over a SLURM infraestruture

> *WARNING* You need to be in a SLURM head-node in order to run this last step

```bash
mpicc -o mpitest mpitest.c
sbatch -N 2 submit.sh
```
