# Installation

**NOTE**: Kind does not require kubectl, but you will not be able to perform some of the examples in our docs without it. To install kubectl, see the [ kubectl installation docs]([https://kubernetes.io/docs/tasks/tools/install-kubectl/](https://github.com/mashby2022/Kubernetes-troubleshooting-Oreilly/blob/main/labs/kubectl%20install.md)).

If you are a Go developer, you may find the `go install` option convenient. Otherwise, we supply downloadable release binaries, community-managed packages, and a source installation guide.

## Installing With A Package Manager

The kind community has enabled installation via the following package managers.

### On macOS via Homebrew:

```bash
brew install kind
```

### On macOS via MacPorts:

```bash
sudo port selfupdate && sudo port install kind
```

### On Windows via Chocolatey (Chocolatey kind package):

```bash
choco install kind
```

## Installing From Release Binaries

Pre-built binaries are available on our [releases page](https://github.com/kubernetes-sigs/kind/releases).

To install, download the binary for your platform from "Assets," then rename it to kind (or perhaps kind.exe on Windows) and place this into your $PATH at your preferred binary installation directory.

### On Linux:

```bash
# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### On macOS:

```bash
# For Intel Macs
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-darwin-amd64
# For M1 / ARM Macs
[ $(uname -m) = arm64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-darwin-arm64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind
```

### On Windows in PowerShell:

```powershell
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.20.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
```

## Installing From Source

In addition to the pre-built binary + package manager installation options listed above, you can install kind from source with `go install sigs.k8s.io/kind@v0.20.0` or clone this repo and run `make build` from the repository.

### Installing With make

Using `make build` does not require installing Go and will build kind reproducibly. The binary will be in `bin/kind` inside your clone of the repo.

You should only need `make` and standard userspace utilities to run this build. It will automatically obtain the correct Go version with our vendored copy of `gimme`.

You can then call `./bin/kind` to use it, or copy `bin/kind` into some directory in your system `$PATH` to use it as kind from the command line.

`make install` will attempt to mimic `go install` and has the same path requirements as `go install` below.

### Installing with go install

When installing with Go, please use the latest stable Go release. At least go1.16 or greater is required.

To install use: `go install sigs.k8s.io/kind@v0.20.0`.

If you are building from a local source clone, use `go install .` from the top-level directory of the clone.

`go install` will typically put the kind binary inside the `bin` directory under `go env GOPATH`, see Go's ["Compile and install packages and dependencies"](https://golang.org/doc/code.html#GOPATH) for more on this. You may need to add that directory to your `$PATH` if you encounter the error `kind: command not found` after installation; you can find a guide for adding a directory to your PATH [here](https://gist.github.com/nex3/c395b2f8fd4b02068be37c961301caa7#file-path-md).

# Creating a Cluster

Creating a Kubernetes cluster is as simple as `kind create cluster`.

This will bootstrap a Kubernetes cluster using a pre-built node image. Prebuilt images are hosted at `kindest/node`, but to find images suitable for a given release, currently, you should check the release notes for your given kind version (check with `kind version`) where you'll find a complete listing of images created for a kind release.

To specify another image, use the `--image` flag – `kind create cluster --image=....`.

Using a different image allows you to change the Kubernetes version of the created cluster.

If you desire to build the node image yourself with a custom version, see the building images section.

By default, the cluster will be given the name `kind`. Use the `--name` flag to assign the cluster a different context name.

If you want the `create cluster` command to block until the control plane reaches a ready status, you can use the `--wait` flag and specify a timeout. To use `--wait`, you must specify the units of the time to wait. For example, to wait for 30 seconds, do `--wait 30s`, for 5 minutes do `--wait 5m`, etc.

More usage can be discovered with `kind create cluster --help`.

# Interacting with Your Cluster

After creating a cluster, you can use `kubectl` to interact with it by using the configuration file generated by Kind.

## Default Cluster Configuration

By default, the cluster access configuration is stored in `${HOME}/.kube/config` if the `$KUBECONFIG` environment variable is not set.

If the `$KUBECONFIG` environment variable is set, it is used as a list of paths (following normal path delimiting rules for your system). These paths are merged, with modifications occurring in the file that defines the stanza. If a value is created, it is placed in the first existing file in the list. If none of the files in the chain exist, the configuration is created in the last file in the list.

## Custom Kubeconfig

You can use the `--kubeconfig` flag when creating the cluster to specify a custom kubeconfig file. In this case, only that specified file is loaded, and no merging takes place.

## Listing Clusters

To see all the clusters you have created, you can use the `kind get clusters` command.

For example, let’s say you create two clusters:

```bash
kind create cluster # Default cluster context name is 'kind'.
...
kind create cluster --name kind-2
```

When you list your kind clusters, you will see something like the following:

```bash
kind get clusters
kind
kind-2
```

## Interacting with a Specific Cluster

To interact with a specific cluster, you only need to specify the cluster name as a context in `kubectl`. For example:

```bash
kubectl cluster-info --context kind-kind
kubectl cluster-info --context kind-kind-2
```

# Deleting a Cluster

If you created a cluster with `kind create cluster`, deleting it is equally simple:

```bash
kind delete cluster
```
If the `--name` flag is not specified, Kind will use the default cluster context name, 'kind,' and delete that cluster.







