# Elastic stack for Kubernetes observability (Elasticsearch, Filebeat, Metricbeat and Kibana)

## What is this?
This repo is a bundle of the elastic stack for Kubernetes observability. It contains 4 elastic products:

* Elasticsearch - Cluster of 3 nodes that will hold all of the data and provide search abilities
* Kibana - The UI to explore and visualize our data
* Filebeat - The agent that will run on all of the cluster nodes, process and enrich and save logs to elasticsearch
* Metricbeat - The agent that will run on all nodes and collect CPU and Memory metrics
* kube-state-metrics - Stats agent that gets metrics from k8s API - some metrics are used by Metricbeat

## Usage
All of the stack will run under the `logging` namespace. To deploy all of it, start with deploying the namespace, then, all others.

* Deploying the namespace: `kubectl apply -f namespace/namespace.yaml`
* Deploying the elastic components: `kubectl apply -R -f elastic/ -f filebeat/ -f kibana/ -f metricbeat/ -f kube-state-metrics/`
* Make sure all pods are ready: `kubectl -n logging get po`

To access the kibana UI you can create a proxy using kubectl: 

`kubectl -n logging port-forward service/kibana 5601`

And point your browser to [http://localhost:5601](http://localhost:5601)