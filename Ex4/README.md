# Exercise 4 : Policy Reporter UI Installation
In this exercise each student will install Kyverno's Policy Reporter UI on an Openshift cluster;

## Objective
To install Policy Reporter UI on a Kubernetes/Openshift cluster from a local Helm chart.

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
   - Obtain the Kyverno UI Helm chart package (e.g., `.tgz` or `.tar.gz`) and place it in a local folder accessible on your machine (e.g., `policy-reporter/`).
   ```bash
   helm repo add policy-reporter https://kyverno.github.io/policy-reporter
   helm repo update

   helm pull policy-reporter/policy-reporter
   
   ls 

   # --- output ---
   # policy-reporter-XXX.tgz 

   tar xvzf policy-reporter-*
   
   cd policy-reporter
   ```

4. **Edit the `values.yaml` files of the policy reporter and its dependencies charts:**
   - Run:
   ```bash
   yq -i 'del(.podSecurityContext)' values.yaml
   yq -i ".podSecurityContext={}" values.yaml
   yq -i 'del(.securityContext)' values.yaml
   yq -i ".securityContext={}" values.yaml
   yq -i 'del(.securityContext)' charts/kyvernoPlugin/values.yaml
   yq -i ".securityContext={}" charts/kyvernoPlugin/values.yaml
   yq -i 'del(.securityContext)' charts/ui/values.yaml
   yq -i ".securityContext={}" charts/ui/values.yaml
   ```
   - Make sure the output of the following command is empty:
   ```bash
   helm template . -f values.yaml  | grep -i securitycontext
   ```

5. **Add the Policy Reporter Helm chart from the local folder:**
   - From the `policy-reporter` directory, run the following command to install the Policy-Reporter Helm chart from the local folder:
   ```bash
   helm install policy-reporter . -n kyverno
   ```
   - Wait for the installation to complete. You can check the status using `helm ls -n kyverno` or `kubectl get pods -n kyverno` to see if all the Kyverno components are running.
   - Desired Output:
   ```bash
   helm ls -n kyverno

   # OUTPUT
   # NAME   	           NAMESPACE	REVISION	STATUS  	CHART        	APP VERSION
   # kyverno	           kyverno  	1       	deployed	kyverno-x.x.x	vx.x.x     
   # policy-reporter      kyverno   1        deployed 
   ```
6. **Verify the Policy Reporter installation:**
   - Check if the **3** Policy Reporter pods are running by running `kubectl get pods -n kyverno`.
   - Ensure all the pods are in a "Running" state.
   ```bash
   kubectl get pods -n kyverno

   # OUTPUT
   # NAME                             READY   STATUS    
   # kyverno-xxx                      1/1     Running   
   # kyverno-xxx                      1/1     Running   
   # kyverno-xxx                      1/1     Running   
   # kyverno-cleanup-controller-xxx   1/1     Running
   
   ```

7. Access the Policy Reporter UI page
   ```bash
   oc get route -n kyverno --no-headers | awk '{print "https://"$2}'
   ```

8. Run Exercise 2 again, and this time don't delete the policies. Once deployed, access the Policy Reporter and see the results.

Congratulations! You have successfully installed Policy Reporter on your Kubernetes cluster using the Helm chart from a local folder.

