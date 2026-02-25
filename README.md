# Brood chamber

This repository contains Helm charts that I've built for my personal use within [my Apiary cluster](https://github.com/CSchoel/apiary/tree/main).

## Installation

* [Install Helm](https://helm.sh/docs/intro/install/).
* Set up your kubernetes cluster.

### Charts in this repo

* Run `helm install lt charts/languagetool`.
* To upgrade run `helm upgrade lt charts/languagetool`.

### GitLab

```bash
# reference: https://docs.gitlab.com/charts/installation/deployment/
helm repo add gitlab https://charts.gitlab.io/
helm repo update
helm install gitlab gitlab/gitlab -f external/gitlab/values.yaml
```

#### Debugging

* To check `nginx-ingress` config:
  * `kubectl exec -it gitlab-nginx-ingress-controller-CHOOSE_POD_HERE -- cat /etc/nginx/nginx.conf`
