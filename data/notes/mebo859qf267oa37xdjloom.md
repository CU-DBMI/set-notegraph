
## Summary

[Dagger](https://docs.dagger.io/) by default will attempt to use Docker installations but does not require Docker to run. Some customization without using Docker is covered on the following page: [Customizing your Buildkit installation](https://docs.dagger.io/1223/custom-buildkit/). The following covers how to use Dagger with containerized Buildkit using Podman.

## Steps

1. [Install Podman](https://podman.io/getting-started/installation)
1. Run Buildkit using the following, modifying as appropriate for your system: `podman run -d --name buildkitd --privileged -p 1234:1234 moby/buildkit:latest --addr tcp://0.0.0.0:1234` ([reference](https://github.com/moby/buildkit#podman) and [issue for podman explicit ports](https://github.com/dagger/dagger/issues/1959#issuecomment-1101547522))
1. [Install Dagger](https://docs.dagger.io/1200/local-dev)
1. Set BUILDKIT_HOST environment variable to podman-container://buildkit , for ex: `export BUILDKIT_HOST=tcp://localhost:1234` ([reference](https://docs.dagger.io/1223/custom-buildkit/) and [issue for podman explicit ports](https://github.com/dagger/dagger/issues/1959#issuecomment-1101547522))
1. Run Dagger commands as necessary.
