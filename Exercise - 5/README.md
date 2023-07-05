# Exercise 5: Part 1 - Installing ACM
Follow the medium document and install acm via the UI in the Operator MarketPlace 
[Link to קגןוצ](https://medium.com/@hillayamir/installation-and-basic-configuration-for-redhats-advanced-cluster-management-drill-down-for-62d3d9c903f8)


# Exercise 5: Part 2 - Installing Kyverno with ACM

## Objective
Install Kyverno operator (from a git hosted Helm chart) on top of 1/or more Openshift clusters using RHACM and cluster "labels".

[Link to the opensource project](https://kyverno.github.io/policy-reporter/)

# Notes!
1. We are going to pull the Policy Reporter UI `helm chart` locally and edit the values file to fit our demands. This is also the procedure to install it in a disconnected environment.

2. For a full disconnected environment installation you should also pull the Kyverno `image` and import it to the disconnected network alongside the helm chrat itself.

## Prerequisites
- A running Kubernetes/Openshift cluster
- Helm v3 or later installed on your local machine
- The Policy Reporter UI Helm chart package available in a local folder (e.g., `policy-reporter/`)
- yq binary installed on your machine

## Steps
1. **Install yq:**
   ```bash
   sudo wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64
   sudo chmod a+x /usr/local/bin/yq
   ```

2. **Pull the Kyverno UI Helm chart:**
   - Ob
   ```

8. Run Exercise 2 again, and this time don't delete the policies. Once deployed, access the Policy Reporter and see the results.

Congratulations! You have successfully installed Policy Reporter on your Kubernetes cluster using the Helm chart from a local folder.

