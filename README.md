# Hybrid_cloud_ecosystems

```vars.yml
username: {{ user }}

```

## Deploy Submariner

## Configure Submariner

## Deploy Skupper Operator

```sh
# Create a Project
oc new-project "{{ username }}"

# Creating a CatalogSource in the `openshift-marketplace` namespace
oc apply -f ocp/00-CatalogSource.yaml

# Wait for the skupper-operator catalog pod to be running
oc -n openshift-marketplace get pods | grep skupper-operator

# Create an OperatorGroup in the `my-namespace` namespace
oc apply -f ocp/10-OperatorGroup.yaml

# Create a Subscription in the `my-namespace` namespace
oc apply -f ocp/20-Subscription.yaml
```

## Configure Skupper

## Deploy applications

## Scenarios

### Hybrid Cloud Balancing

### DRP

### Backup
