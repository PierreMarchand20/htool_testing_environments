# Testing environments for [Htool](https://github.com/PierreMarchand20/htool) ![Docker building](https://github.com/htool-ddm/htool_testing_environments/workflows/Building%20Docker%20images/badge.svg)

Eight environments are defined via Docker images to test [Htool](https://github.com/PierreMarchand20/htool) with several MPI implementations:

- Ubuntu with `clang` and `OpenMPI`
- Ubuntu with `clang` and `MPICH`
- Ubuntu with `gcc` and `OpenMPI`
- Ubuntu with `gcc` and `MPICH`
- Debian with `clang` and `OpenMPI`
- Debian with `clang` and `MPICH`
- Debian with `gcc` and `OpenMPI`
- Debian with `gcc` and `MPICH`

The Docker images can be pulled from [Docker Hub](https://hub.docker.com/r/pierremarchand/htool_testing_environments). We use GitHub Action to build and push these images to Docker Hub.
