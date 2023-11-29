# Hybrid_cloud_ecosystems

## Deploy Submariner

## Configure Submariner

## Deploy Skupper Operator

```sh
# Creating a CatalogSource in the `openshift-marketplace` namespace
kubectl apply -f examples/ocp/00-cs.yaml

# Wait for the skupper-operator catalog pod to be running
kubectl -n openshift-marketplace get pods | grep skupper-operator

# Create an OperatorGroup in the `my-namespace` namespace
kubectl apply -f examples/ocp/10-og.yaml

# Create a Subscription in the `my-namespace` namespace
kubectl apply -f examples/ocp/20-sub.yaml
```

## Configure Skupper

## Deploy applications

## Scenarios

### Hybrid Cloud Balancing

### DRP

### Backup
