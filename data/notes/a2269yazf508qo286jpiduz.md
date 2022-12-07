
## Summary

Projects which use [Dagger](https://docs.dagger.io/) must be initialized to include dependencies from the core library in order to run. While it's recommended to include these dependencies as part of the project ([reference](https://docs.dagger.io/1225/pushing-plan-dependencies/)), there are sometimes many additional files included as part of this (any possible dependency is included, instead of those referenced only). See the below for getting started with a dagger project.

## Steps

1. Create a `<name>.cue` file to include your custom Dagger work.
1. Use command `dagger project init` from within the same dir as the cue file.
1. There are sometimes issues with project init, and you may also need to use `dagger project update` immediately after initializing your project.
1. Use command `dagger do <action name>` as needed.
