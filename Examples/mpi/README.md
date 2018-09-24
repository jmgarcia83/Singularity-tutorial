Submit mpi example over a SLURM infraestruture

```bash
mpicc -o mpitest mpitest.c
sbatch -N 2 submit.sh
```