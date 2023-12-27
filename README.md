Lo modifico para hacer pull request!

# <b>Creating and running software containers with Singularity</b>
### <i>How to use [Singularity](https://www.sylabs.io/)! </i>

<img src="Assets/SingularityLogo.png" width="250">

- [Singularity Home](https://www.sylabs.io/)
- [Singularity on GitHub](https://github.com/sylabs/singularity)
- [Singularity on Google Groups](https://groups.google.com/a/lbl.gov/forum/#!forum/singularity)
- [Sylabs Library](https://cloud.sylabs.io/library)

## Introduction

### What IS a software container anyway? (And what's it good for?)

A container allows you to stick an application and all of its dependencies into a single package.  This makes your application portable, shareable, and reproducible.

Containers foster portability and reproducibility because they package **ALL** of an applications dependencies... including its own tiny operating system!

This means your application won't break when you port it to a new environment. Your app brings its environment with it.

Here are some examples of things you can do with containers:

- Package an analysis pipeline so that it runs on your laptop, in the cloud, and in a high performance computing (HPC) environment to produce the same result.
- Publish a paper and include a link to a container with all of the data and software that you used so that others can easily reproduce your results.
- Install and run an application that requires a complicated stack of dependencies with a few keystrokes.
- Create a pipeline or complex workflow where each individual program is meant to run on a different operating system.

### How do containers differ from virtual machines (VMs)

Containers and VMs are both types of virtualization.  But it's important to understand the differences between the two and know when to use each.

**Virtual Machines** install every last bit of an operating system (OS) right down to the core software that allows the OS to control the hardware (called the _kernel_).  This means that VMs:
- Are complete in the sense that you can use a VM to interact with your computer via a different OS.
- Are extremely flexible.  For instance you an install a Windows VM on a Mac using software like [VirtualBox](https://www.virtualbox.org/wiki/VirtualBox).
- Are slow and resource hungry.  Every time you start a VM it has to bring up an entirely new OS.

**Containers** share a kernel with the host OS.  This means that Containers:
- Are less flexible than VMs.  For example, a Linux container must be run on a Linux host OS.  (Although you can mix and match distributions.)  In practice, containers are only extensively developed on Linux.
- Are much faster and lighter weight than VMs.  A container may be just a few MB.
- Start and stop quickly and are suitable for running single apps.

Because of their differences, VMs and containers serve different purposes and should be favored under different circumstances.
- VMs are good for long running interactive sessions where you may want to use several different applications.  (Checking email on Outlook and using Microsoft Word and Excel).
- Containers are better suited to running one or two applications non-interactively in their own custom environments.

### Singularity

[Singularity](https://www.sylabs.io/) is a 3 years container runtime software originally developed by Greg Kurtzer while at Lawrence Berkley National labs.  It was developed with security, scientific software, and HPC systems in mind.

**philosophy**

Singularity assumes ([more or less](http://containers-ftw.org/SCI-F/)) that each application will have its own container.  It does not seek to fully isolate containers from one another or the host system.
Singularity assumes that you will have a build system where you are the root user, but that you will also have a production system where you may or may not be the root user.

**strengths**
- Easy to learn and use (relatively speaking)
- Approved for HPC (installed on some of the biggest HPC systems in the world)
- Can convert Docker containers to Singularity and run containers directly from Docker Hub
- Sylabs container Library [Sylabs Library](https://cloud.sylabs.io/library)
- [Singularity Hub](https://singularity-hub.org/)!
    - A place to build and host your containers similar to Docker Hub

Singularity shines for scientific software running in an HPC environment.  We will use it for the remainder of the class.

## Tutorial steps

 - [Step 1 - Install](INSTALL.md)
 - [Step 2 - Build and Run](BUILD_RUN.md)
 - [Step 3 - Cloud services](CLOUD_SERVICES.md)
 - [Step 4 - Instances](INSTANCES.md)
 - [Step 5 - GPU](GPU.md)

Want to learn more:
 - [Miscellaneous](MISCELLANEOUS.md)
 - [Join the community](https://www.sylabs.io/singularity/join-the-community/)
