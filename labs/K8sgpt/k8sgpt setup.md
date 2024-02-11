# Introduction to K8sGPT: Installation Guide

K8sGPT is an open source tool designed to empower Kubernetes Site Reliability Engineers (SREs) with advanced capabilities. It simplifies the process of scanning Kubernetes clusters and diagnosing issues by providing analysis in plain English. The tool is engineered to encapsulate SRE expertise into its analyzers, allowing it to extract pertinent information and enhance it with AI.

K8sGPT leverages the power of ChatGPT for Kubernetes platforms. It enables users to analyze cluster issues and receive detailed reports with suggestions for resolution.

## Installation

### Linux/Mac via Brew

#### Prerequisites

Ensure you have Homebrew installed:

- [Homebrew for Mac](https://brew.sh)
- [Homebrew for Linux](https://docs.brew.sh/Homebrew-on-Linux)

#### Installation

Install K8sGPT on your machine with the following commands:

```bash
brew tap k8sgpt-ai/k8sgpt
brew install k8sgpt
```

### Other Installation Options

#### RPM-based Installation (RedHat/CentOS/Fedora)

- For 32-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_386.rpm
  sudo rpm -ivh k8sgpt_386.rpm
  ```

- For 64-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_amd64.rpm
  sudo rpm -ivh -i k8sgpt_amd64.rpm
  ```

#### DEB-based Installation (Ubuntu/Debian)

- For 32-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_386.deb
  sudo dpkg -i k8sgpt_386.deb
  ```

- For 64-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_amd64.deb
  sudo dpkg -i k8sgpt_amd64.deb
  ```

#### APK-based Installation (Alpine)

- For 32-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_386.apk
  apk add k8sgpt_386.apk
  ```

- For 64-bit systems:
  ```bash
  curl -LO https://github.com/k8sgpt-ai/k8sgpt/releases/download/v0.3.24/k8sgpt_amd64.apk
  apk add k8sgpt_amd64.apk
  ```

### Windows

Download the latest Windows binaries of K8sGPT from the [Release tab](https://github.com/k8sgpt-ai/k8sgpt/releases) based on your system architecture. Extract the downloaded package to your desired location and configure the system path variable with the binary location.

### Verify Installation

Verify that K8sGPT is installed correctly by running:

```bash
k8sgpt version
```

You should see output similar to:

```bash
k8sgpt version 0.2.7
```

## Sample Exercise

To illustrate K8sGPT's capabilities, let's go through a sample exercise:

### Prerequisites

Ensure K8sGPT is installed correctly on your environment by following the installation instructions above. Additionally, make sure you are connected to a Kubernetes cluster and have `kubectl` installed.

### Setting up a Kubernetes Cluster

To try out K8sGPT, set up a basic Kubernetes cluster such as KinD (Kubernetes in Docker) or Minikube if you're not connected to any other cluster.

#### Creating a KinD Kubernetes Cluster

Install KinD first:

```bash
brew install kind
```

Create a new Kubernetes cluster:

```bash
kind create cluster --name k8sgpt-demo
```

### Using K8sGPT

You can view different command options through:

```bash
k8sgpt --help
```

To authenticate with OpenAI, generate a token from the backend:

```bash
k8sgpt generate
```

Authenticate with the generated token:

```bash
k8sgpt auth add --backend openai --model gpt-3.5-turbo
```

Analyze your cluster:

```bash
k8sgpt analyze
```

This command will generate a list of issues present in your Kubernetes cluster. For instance, creating a "broken Pod" and analyzing it will result in an error message highlighting the problem related to the container image.

Congratulations! You have successfully created a local Kubernetes cluster, deployed a "broken Pod," and analyzed it using K8sGPT.
```
