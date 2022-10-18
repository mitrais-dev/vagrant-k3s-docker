# K3S Cluster

This vagrant will create one virtual machine for Kubernetes Control Plane and Docker Server.
The default IP Address is `192.168.2.100` see details in `Vagrantfile`.

## Ingredient

- [Vagrant](https://www.vagrantup.com/downloads)
- [Kubernetes Command-Line Tool](https://kubernetes.io/docs/tasks/tools/)
- Docker Client

> Note: Docker Client can be installed using [Chocolatey](https://community.chocolatey.org/packages/docker) or [Scoop](https://scoop.sh/#/apps?q=docker&s=0&d=1&o=true)

## How to run

- Execute `vagrant up` to start the virtual machines. First time start will setup Docker server & K3S cluster.
- Modify generated `k3s.yaml`, change the server IP Address to point to virtual machine.

  ```yaml
  - cluster:
      server: https://IP:6443
  ```

Test with kubectl using `k3s.yaml` as config:

```console
kubectl --kubeconfig k3s.yaml version
```

Test with Docker Client:

```console
set DOCKER_HOST=192.168.2.100
docker version
```

## Deploy Sample Appplication

Execute `kubectl --kubeconfig sample-deployment.yaml`.
The application can be accessed through `http://IP`.

## TIPS

If you are not familiar with `kubectl` command you can use [Octant](https://octant.dev) to view the cluster.
Execute `octant --kubeconfig k3s.yaml` and octant will be available in <http://127.0.0.1:7777>