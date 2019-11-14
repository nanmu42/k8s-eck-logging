# K8S Logging

Kubernetes cluster level logging solution, utilizing Elasticseach, Kibana and Fluent Bit.

# Prerequisites

* Kubernetes 1.12 or higher (minikube not working)
* Predefined storage class called `hdd-ssd` (you may change it in `eck.yaml`)

# Quick Start (Mini-sized Deployment)

* Clone This Repo

* Deploy Elastic Cloud on Kubernetes(ECK)

For Kubernetes clusters running version 1.13 or higher:

```bash
kubectl create -f https://download.elastic.co/downloads/eck/1.0.0-beta1/all-in-one.yaml
```

For Kubernetes clusters running version 1.12 or lower:

```bash
kubectl create -f https://download.elastic.co/downloads/eck/1.0.0-beta1/all-in-one-no-validation.yaml
```

* Create Namespace `logging`

```bash
kubectl create -f ./namespace.yml
```

* Deploy Elasticsearch and Kibana

```bash
kubectl create -f ./eck.yml
```

* Deploy Fluent Bit

```bash
kubectl create -f fluent-bit-service-account.yaml
kubectl create -f fluent-bit-role.yaml
kubectl create -f fluent-bit-role-binding.yaml
kubectl create -f fluent-bit-configmap.yaml
kubectl create -f fluent-bit-ds.yaml
```

And off you go. :rocket:

# Reference

* [Elastic Cloud on Kubernetes](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-quickstart.html)
* [Kubernetes Logging with Fluent Bit](https://github.com/fluent/fluent-bit-kubernetes-logging)
* [Fluent Bit Manual](https://docs.fluentbit.io/manual/output/elasticsearch)
* [Enabling Native Realms on ECK](https://github.com/elastic/cloud-on-k8s/issues/2036#issuecomment-544838578)
* [A Realms Bug in ECK 1.0.0](https://github.com/elastic/cloud-on-k8s/issues/2036#issuecomment-544838578)