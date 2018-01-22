# How to use your Kubernetes remote control, or: kubectl in action

Talk at [Pre-FOSDEM warmup with Kubernetes](https://www.meetup.com/Brussels-Kubernetes-Meetup/events/245974093/) at Brussels Kubernetes Meetup, 2018-02-02.

Kubernetes comes with kubectl, a CLI that allows you to interact with your cluster, supporting operations from config to managing workloads to administrative tasks. In this talk you'll learn everything you need to know getting the most out of kubectl and beyond.

## Setup

```
$ kubectl config
```

## Docs and config

What was that field in the manifest again?

```
$ kubectl explain statefulset.spec.template.spec
```

List contexts:

```
$ kubectl config get-contexts
```

## Workloads

Simple jump pod:

```
$ kubectl run -i -t --rm jump --image=quay.io/mhausenblas/jump:v0.1 -- sh
```

Name of pod(s) labelled with `app=example`:

```
$ kubectl get po -l=app=example -o=custom-columns=:metadata.name --no-headers
```

## Accessing the API

```
$ kubectl proxy
```

### RBAC

Can a certain SA list pods?

```
$ kubectl auth can-i list pods --as=system:serviceaccount:sec:myappsa
```

Create rolebinding for an SA in a specified namespace and just do a dry run:

```
$ kubectl create rolebinding podreaderbinding --role=sec:podreader --serviceaccount=sec:myappsa --namespace=sec --dry-run=true -o=yaml -n=sec
```

## Debugging

```
$ kubectl get events
$ kubectl logs
```

## Tips and tricks

- Install and use [auto-complete](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion)
- set `KUBE_EDITOR` to your favorite editor

Tools that extend and enhance `kubectl`:

- https://github.com/jonmosco/kube-ps1
- https://github.com/ahmetb/kubectx
- https://github.com/cloudnativelabs/kube-shell
- https://github.com/nii236/kk
- http://kubed.sh/
