# Kubernetes Custom Controller - Custom Resource Handling

**Note**: the source code is _verbosely_ commented, so the source is meant to be read and to teach

## What is this?

An example of a custom Kubernetes controller that's only purpose is to watch for the creation, updating, or deletion of all custom resource of type `Network` (in the all namespaces). This was created as an exercise to understand how Kubernetes controllers work and interact with the cluster and resources.

## Running

Clone repo:

```
$ git clone https://github.com/YTGhost/k8s-controller-custom-resource
$ cd k8s-controller-custom-resource
```

Prepare build environment:

```
go mod vendor
```

Build and run:

```
go build -o samplecrd-controller .
./samplecrd-controller -kubeconfig=$HOME/.kube/config -alsologtostderr=true
```

## Usage

You should create the CRD of Network first:

```
kubectl apply -f crd/network.yaml
or
kubectl apply -f crd/network-1.22+.yaml # for 1.22+
```

You can then trigger an event by creating a Network API instance:

```
kubectl apply -f example/example-network.yaml
```

CURD the Network API instance, and check the logs of controller. 

Enjoy!

## Code generation

You should modify the `hack/update-codegen.sh` file to your needs first.

And then run:

```
./hack/update-codegen.sh
```

It will help you to generate the code for the CRD: deepcopy funcs, clientset, listers, informers.