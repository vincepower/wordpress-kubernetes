# Simple WordPress deployment on OpenShift

## Containers used
- [WordPress (Latest)](https://hub.docker.com/_/wordpress/)
- [MySQL (5.7)](https://hub.docker.com/_/mysql/)

## Prerequisite

A running OpenShift cluster with a default storage class and a default project set.

## Objectives

This scenario provides instructions for the following tasks:

- Create a secret to protect sensitive data.
- Create and deploy the WordPress frontend with one or more pods.
- Create and deploy the MySQL database

## Deply to Kubernetes

`kustomize` lets you customize raw, template-free YAML
files for multiple purposes, leaving the original YAML
untouched and usable as is.

Update kustomize.yaml and replace YOUR_PASSWORD with a password which will be used for MySQL (Could be any string with ASCII characters).

### To run the kustomization file 

```bash
oc apply -k ./
```

```bash
secret/mysql-pass-8mbg69d8ch created
service/wordpress-mysql created
service/wordpress created
deployment.apps/wordpress-mysql created
deployment.apps/wordpress created
route.route.openshift.io/wordpress created
persistentvolumeclaim/mysql-pv-claim created
persistentvolumeclaim/wp-pv-claim created
```

### To remove the deployment

```bash
oc delete -k ./
```

#### Check your added replica
```bash
$ oc get deployments
NAME              DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
wordpress         2         2         2            2           23h
wordpress-mysql   1         1         1            1           23h
```

