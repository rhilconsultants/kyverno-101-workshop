# Exercise 1 : Installing Kyverno Helm Chart on Kubernetes Cluster

## Objective
To install Kyverno, a Kubernetes native policy management tool, using the Helm package manager on a Kubernetes/Openshift cluster from a local Helm chart.

[Link to the opensource project](https://kyverno.io/)

# Notes!
1. We are going to pull the Kyverno `helm chart` locally and edit the values file to fit our demands. This is also the procedure to install it in a disconnected environment.

2. For a full disconnected environment installation you should also pull the Kyverno `image` and import it to the disconnected network alongside the helm chrat itself.

## Prerequisites
- A running Kubernetes/Openshift cluster
- Helm v3 or later installed on your local machine
- The Kyverno Helm chart package available in a local folder (e.g., `kyverno/`)

## Steps

1. **Setup the Kubernetes cluster:**
   - Ensure you have a Kubernetes/Openshift cluster up and running. You can use a local cluster like Minikube or a cloud provider's managed Kubernetes service like GKE, EKS, or AKS.
   - Connect to the cluster using the appropriate tools (e.g., `kubectl`/`oc`).
   
2. **Install Helm:**
   - Make sure Helm is installed on your local machine. You can verify by running the command `helm version`.
   - If Helm is not installed, follow the [official Helm installation](https://helm.sh/docs/intro/install/) instructions for your operating system.

3. **Pull the Kyverno Helm chart:**
   - Obtain the Kyverno Helm chart package (e.g., `.tgz` or `.tar.gz`) and place it in a local folder accessible on your machine (e.g., `kyverno/`).
   ```bash
   helm repo add kyverno https://kyverno.github.io/kyverno/
   helm repo update

   helm pull kyverno/kyverno
   
   ls 

   # --- output ---
   # kyverno-XXX.tgz 

   tar xvzf kyverno-*
   
   cd kyverno

   vi values.yaml
   ```

4. **Edit the `values.yaml` file:**
   - Open the `values.yaml` file located in the Kyverno Helm chart directory.
   - Find the `replicaCount` field and set its value to `3` to make the Kyverno deployment highly available.
   - Save the changes.
   > Shortcut: ```sed -i 's/^replicaCount.*/replicaCount: 3/' values.yaml```

5. **Add the Kyverno Helm chart from the local folder:**
   - From the `kyverno` directory, run the following command to install the Kyverno Helm chart from the local folder:
   ```bash
   helm install kyverno . -f values.yaml -n kyverno --create-namespace
   ```
   - Wait for the installation to complete. You can check the status using `helm ls -n kyverno` or `kubectl get pods -n kyverno` to see if all the Kyverno components are running.
   - Desired Output:
   ```bash
   helm ls -n kyverno

   # OUTPUT
   # NAME   	NAMESPACE	REVISION	STATUS  	CHART        	APP VERSION
   # kyverno	kyverno  	1       	deployed	kyverno-x.x.x	vx.x.x     
   ```
6. **Verify the Kyverno installation:**
   - Check if the Kyverno pods are running by running `kubectl get pods -n kyverno`.
   - Ensure all the Kyverno pods are in a "Running" state.
   ```bash
   kubectl get pods -n kyverno

   # OUTPUT
   # NAME                             READY   STATUS    
   # kyverno-xxx                      1/1     Running   
   # kyverno-xxx                      1/1     Running   
   # kyverno-xxx                      1/1     Running   
   # kyverno-cleanup-controller-xxx   1/1     Running   
   
   ```


Congratulations! You have successfully installed Kyverno on your Kubernetes cluster using the Helm chart from a local folder, with a highly available Kyverno deployment.

> Note: If you encounter any issues during the installation, ensure that the Kyverno Helm chart package is correctly placed in the specified local folder. Refer to the Kyverno documentation or seek assistance from the instructor or online communities for troubleshooting.

