---
title: 'AKS and Policy Insights'
date: 2021-04-23
categories: [IT]
tags: [aks, policy, microsoft]
---

## Activate Policy Insights 
```
az provider register --namespace Microsoft.PolicyInsights
```

### Check AKS Kubernetes Version
It must be at least 1.14
```
az aks list | grep kubernetesVersion
```

### Check Azure CLI Version
It must be at least 2.12.0
```
az --version
```

### Enable the azure-policy addon
```
# set your cluster name and the corresponding resourcegroup name
export CLUSTER=MyAKSCluster
export RG=MyResourceGroup

# enable the azure policy addon
az aks enable-addons --addons azure-policy --name $CLUSTER --resource-group $RG
```

### Verify that the add-on installation was successful
```
# we are looking for a azure-policy pod
kubectl get pods -n kube-system

# there should be also pods in a new namespace called gatekeeper-system
kubectl get pods -n gatekeeper-system
```

### Finally, make sure that the latest add-on is installed and v2 is shown
```
az aks show --query addonProfiles.azurepolicy -g $RG -n $CLUSTER
```

### Get the azure-policy pod name installed in kube-system namespace
```
kubectl logs <azure-policy pod name> -n kube-system
```

### Get the gatekeeper pod name installed in gatekeeper-system namespace
```
kubectl logs <gatekeeper pod name> -n gatekeeper-system
```

### What about
**Diagnostic data collected by the Azure Policy add-on.**

The Azure Policy add-on for Kubernetes collects limited cluster diagnostic data.
This diagnostic data is important technical data related to software and performance. It is used for the following purposes:
- Keep Azure Policy Add-On up to date.
- Keep Azure Policy Add-On secure, reliable, and performing well
- Improve Azure Policy Add-On - through aggregate analysis of how the add-on is used.

The information collected by the Add-On is not personal data. The following details are currently collected:
Azure Policy Add-On agent version.
- Cluster type
- Cluster region
- Cluster resource group
- Cluster resource ID
- Cluster subscription ID
- Cluster operating system (example: Linux)
- City for the cluster (example: Seattle)
- State or canton for the cluster (example: Washington)
- Country or region for the cluster (example: USA)

Exceptions/errors encountered during the agent's installation when Azure Policy Add-On is evaluating policies
Number of Gatekeeper policy definitions that were not installed by the Azure Policy Add-On.

## Uninstall the addon
```
az aks disable-addons --addons azure-policy --name $CLUSTER --resource-group $RG
```



