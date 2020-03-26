# Testing environments for [Htool](https://github.com/PierreMarchand20/htool) ![Docker Automated](https://img.shields.io/docker/cloud/automated/pierremarchand/htool_testing_environments) ![Docker Build](https://img.shields.io/docker/cloud/build/pierremarchand/htool_testing_environments)

Four environments are defined via Docker images to test [Htool](https://github.com/PierreMarchand20/htool) with several MPI implementations:

- Ubuntu with `OpenMPI`
- Ubuntu with `MPICH`
- Debian with `OpenMPI`
- Debian with `MPICH`

The Docker images can be pulled from [Docker Hub](https://hub.docker.com/repository/docker/pierremarchand/htool_testing_environments) and there are used by Travis CI [here](https://travis-ci.org/github/PierreMarchand20/htool).

Note that we use `docker-compose` to factorize as much as possible the definition of the environments, so that we had to override the `build` and `push` hooks of Docker Hub for automated build.
