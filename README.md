# Hybrid_cloud_ecosystems

```vars.yml
username: {{ user }}

```

## Deploy Submariner

## Configure Submariner

## Deploy Skupper Operator

If you want to try a cluster-wide installation, you don't need to create the `OperatorGroup` as it is already defined at the destination namespaces, so you just need to create the subscription at the correct namespaces, see below.

```sh
# Create a Project
oc new-project "{{ username }}"

# Creating a CatalogSource in the `openshift-marketplace` namespace
oc apply -f ocp/00-CatalogSource.yaml

# Wait for the skupper-operator catalog pod to be running
oc -n openshift-marketplace get pods | grep skupper-operator

# Create an OperatorGroup in the `my-namespace` namespace
oc apply -f ocp/10-OperatorGroup.yaml


oc apply -f ocp /20-Subscription-cluster.yaml

# Create a Subscription in the `my-namespace` namespace
oc apply -f ocp/20-Subscription.yaml
```

## Configure Skupper

## Deploy applications

## Scenarios

### Hybrid Cloud Balancing

### DRP

### Backup
