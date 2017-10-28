# openshift-s2i-golang

A minimal builder/s2i pair for golang on OpenShift.

## Philosophy

Most s2i builders take the responsibility for both assembling the binaries and 
running them within the same image. Though this is an effective strategy for
those that want to get up and running with building docker images quickly
to the OpenShift platform, it creates bloated binaries with remains from
a build process outside of the final build artifact.

This builder has a simple philosophy. Give me a go binary constructed for linux-amd64
and it will construct a docker image, either base centos7 or rhel7 that will run
this binary.

## Building golang binaries

Now that the Docker image generation has been stripped down and no longer has the
golang language installation, there must be some way to generate binaries from source control
to enter as inputs to the stripped down s2i builder. This is where we will leverage the power of
Jenkins integration to the Kubernetes API to construct a pod template that can build our go
apps into a binary that we can run.

The podTemplate working directory is set somewhere outside of the go path, where the source code 
can be checked out via `checkout scm`, but then the correct gopath can be determined 
via the scm URL without needing to configure `go get` in order to download the source code for the app
itself. There is still the problem of secured dependencies, which would have to be configured in
an addon to this pod template docker image in order for closed-source dependencies to be
installed properly during the `go build` stage.
