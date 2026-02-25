# Brood chamber

This repository contains Helm charts that I've built for my personal use within [my Apiary cluster](https://github.com/CSchoel/apiary/tree/main).

## Installation

* [Install Helm](https://helm.sh/docs/intro/install/).
* Set up your kubernetes cluster.

### Charts in this repo

* Run `helm install lt charts/languagetool`.
* To upgrade run `helm upgrade lt charts/languagetool`.

### GitLab

#### Installation

```bash
# reference: https://docs.gitlab.com/charts/installation/deployment/
helm repo add gitlab https://charts.gitlab.io/
helm repo update
helm install gitlab gitlab/gitlab -f external/gitlab/values.yaml
```

#### Accessing the GitLab instance

In a managed Kubernetes instance, the GitLab webservice would be available behind a load-balancer.
However, in a self-managed cluster, the Kubernetes `LoadBalancer` behaves the same as `NodePort`.
This introduces a few small hurdles to accessing the instance we just deployed:

* We need to use the correct `nodePort`, which you can find by running `kubectl describe service gitlab-nginx-ingress-controller`.
  * 👆 Make sure to get the port for HTTPS, not for HTTP.
* We also need to simulate a DNS entry for `gitlab.h02-bottom-board` by adding the following line to `/etc/hosts`:

    ```plain
    192.168.178.84 gitlab.h02-bottom-board gitlab
    ```

    Replace the IPv4 address with the one of your controlplane (and ensure that it stays fixed and isn't changed by the router every time the node restarts).
* For using the GitLab instance as git remote server, you also need the `nodePort` for SSH. The format to specify that in `git add remote` is a bit ugly: `[git@gitlab.h02-bottom-board:SSH_PORT_GOES_HERE]:kylar/apiary.git`.

#### Upgrade or change in values.yaml

```bash
helm upgrade gitlab gitlab/gitlab -f external/gitlab/values.yaml
```

#### Debugging

* To check `nginx-ingress` config:
  * `kubectl exec -it gitlab-nginx-ingress-controller-CHOOSE_POD_HERE -- cat /etc/nginx/nginx.conf`
