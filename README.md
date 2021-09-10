# Event Driven Solution developer environment setup for mac

Updated 9/9/2021: with the stop of using docker desktop, we need to install
hyperekit and minikube:

```sh
brew install hyperkit
brew install minikube
```

##  Run Kafka Strimzi locally with minikube

* Start minikube

```sh
minikube start --memory=4g --cpus=4 --vm-driver=hyperkit
# enable access to docker daemon
eval $(minikube docker-env)

```
* Create the kafka namespace, and deploy Strimzi CRD

```sh
./installStrimziOperator.sh
```

* Deploy a Kafka Cluster

```sh
kubectl apply -k minikube/strimzi/overlay/
```

* Get IP address of the minikube vm: `minikube ip`, then set a 
mapping in `/etc/hosts` for the kakfa bootstrap URL,  so a `quarkus dev` will be able to connect.
