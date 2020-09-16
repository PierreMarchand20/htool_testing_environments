# Testing environments for [Htool](https://github.com/PierreMarchand20/htool) ![Docker building](https://github.com/htool-ddm/htool_testing_environments/workflows/Building%20Docker%20images/badge.svg)

Four environments are defined via Docker images to test [Htool](https://github.com/PierreMarchand20/htool) with several MPI implementations:

- Ubuntu with `OpenMPI`
- Ubuntu with `MPICH`
- Debian with `OpenMPI`
- Debian with `MPICH`

The Docker images can be pulled from [Docker Hub](https://hub.docker.com/repository/docker/pierremarchand/htool_testing_environments) and there are used by Travis CI [here](https://travis-ci.org/github/PierreMarchand20/htool).

We use GitHub Action to build and push these images to Docker Hub.
