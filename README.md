# Brood chamber

This repository contains Helm charts that I've built for my personal use within [my Apiary cluster](https://github.com/CSchoel/apiary/tree/main).
(It's the brood chamber where new bees are born that will live in my Apiary. 😉)

## Installation

### Requirements

* [Install Helm](https://helm.sh/docs/intro/install/).
* Set up your Kubernetes cluster.

### Install via CLI

```bash
helm repo add brood-chamber https://cschoel.github.io/brood-chamber/
helm install lt brood-chamber/languagetool
```

### Install via Helm Controller

If you use k3s, you can use the [Helm Controller](https://docs.k3s.io/add-ons/helm#using-the-helm-controller) to deploy Helm charts to your cluster.

See the Apiary repo for an [example of a LanguageTool manifest](https://github.com/CSchoel/apiary/blob/c2befb8eedda85165265bbe7dbb4dfcf145cc6d9/configs/kubernetes/apiary-k8s/base/languagetool/languagetool-chart.yaml) installed from the Brood Chamber.
