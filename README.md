# K8S ECK Logging

This walk-through guides you to setup an in-cluster Elasticsearch and Kibana suite, with cluster-level logging data gathered by Fluent Bit. You may access and search logs from every pod in cluster, as long as the workload in pod writes log to `stdout` or `stderr`.

# Prerequisites

* Kubernetes 1.11 or higher (minikube not working)
* Predefined storage class called `hdd-ssd` (you may change it in `eck.yaml`)

# Deployment Steps

Clone [this repo](https://github.com/nanmu42/k8s-eck-logging) to get necessary yaml files.

## Elasticsearch and Kibana

[Elastic Cloud on Kubernetes(ECK)](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-overview.html) is now generally available. ECK makes it easy to deploy Elasticsearch and Kibana on k8s with various topology.

* Deploy ECK

```bash
kubectl apply -f https://download.elastic.co/downloads/eck/1.0.1/all-in-one.yaml
```

* Create Namespace `logging`

```bash
kubectl create -f ./namespace.yml
```

* Deploy Elasticsearch and Kibana

```bash
kubectl create -f ./eck.yml
```

## Fluent Bit

FluentBit runs as DaemonSet on every node in cluster, gathering logs from every workload. FluentBit attach metadata like pod name and label to logs delivered to Elasticsearch.

Well-structured log(in JSON) can be searched/filtered by term in Elasticsearch.

```bash
kubectl create -f fluent-bit-service-account.yaml
kubectl create -f fluent-bit-role.yaml
kubectl create -f fluent-bit-role-binding.yaml
kubectl create -f fluent-bit-configmap.yaml
kubectl create -f fluent-bit-ds.yaml
```

And off you go.

# Reference

* [Elastic Cloud on Kubernetes](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-quickstart.html)
* [Kubernetes Logging with Fluent Bit](https://github.com/fluent/fluent-bit-kubernetes-logging)
* [Fluent Bit Manual](https://docs.fluentbit.io/manual/output/elasticsearch)
* [Enabling Native Realms on ECK](https://github.com/elastic/cloud-on-k8s/issues/2036#issuecomment-544838578)
* [Fluent Bit: Elasticsearch output should probably not use a type (flb_type) ](https://github.com/fluent/fluent-bit/issues/1359#issuecomment-553228448)
