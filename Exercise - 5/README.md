# Exercise 5: Part 1 - Installing ACM
Follow the medium document and install acm via the UI in the Operator MarketPlace 
[Link to Medium](https://medium.com/@hillayamir/installation-and-basic-configuration-for-redhats-advanced-cluster-management-drill-down-for-62d3d9c903f8)


# Exercise 5: Part 2 - Installing Kyverno with ACM

## Objective
Install Kyverno operator (from a git hosted Helm chart) on top of 1/or more Openshift clusters using RHACM and cluster "labels".

---

## Explainer
By using RHACM an Openshift administrator can:
* Centrally create, update and delete Kubernetes clusters across multiple private and public clouds
* Hibernate / Resume OCP Clusters across your domain
* Configure Cluster Sets & Cluster Pools for simplified OCP cluster management
* Search, find and modify any kubernetes resource across the entire domain
* Quickly troubleshoot and resolve issues across your federated domain
* Centrally set & enforce policies for security, applications, & infrastructure
* Quickly visualize detailed auditing on configuration of apps and clusters 
* Perform remediation actions by leveraging Ansible Automation Platform integration.
* Built-in compliance policies and audit checks, including GitOps Integration.
* Immediate visibility into your compliance posture based on your defined standards

# PICTURE HERE!!

## Kyverno & ACM Integration
In order to deploy and manage the Kyverno application life-cycle using helm charts, we will “orchestrate” the local and remote deployment of Kyverno on top of our clusters; we will be using ACM and its application deployment mechanism.

You will need to create the following  5 YAML’s:
* Namespace — which will be created on the remote cluster and in which our ACM policy is going to be deployed
* Channel — Points to the Git Repo where the chart resides
* PlacementRule — Let ACM know on which clusters the application should be deployed onto. 
> In the exercise we will create a dedicated PlacementRule that will tell ACM to deploy Kyverno on "install-kyverno=true" labeled clusters.
* Subscription — Link between the channel and the placementRule and allow us to override some values of the helm chart if needed without editing the one in the repository
* Application — Points to the subscription

> Note! In our demo environment we are using a single Openshift cluster per-student that will function both as ACM Hub cluster and as the managed cluster that we will install Kyverno on. 
> You can see the following [recorded demo](https://www.youtube.com/watch?v=2RkVDzvBN6w) that demonstrates how to import a remote cluster to be managed by RHACM

# PICTURE HERE!!

## Prerequisites
- A running Kubernetes/Openshift cluster with at least 3 master nodes
- Helm v3 or later installed on your local machine

## Steps
1. **Delete any old Kyverno installed on the cluster from the previous exercises**
```bash
oc login <OCP Cluster>
helm list --all-namespaces | grep kyverno
helm uninstall kyvenro -n kyverno
```
   
2. **Install RHACM on the cluster** (Done in Part 1)
3. **Switch to ACM view from the Openshift Web UI**

# PICTURE HERE!!

4. **Go over the following YAMLs with the instractor**
```bash
cd /PATH/to/Exercise 5/YAMLs


cat ns.yaml
cat placementrule.yaml
cat channel.yaml
cat subscription.yaml
cat application.yaml

oc apply -f .
```

5. **Label the local cluster with the label "install-kyverno=true" and see the application is being installed on it by ACM in the appication view**

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/dfe4096e-c70e-4b41-9a72-5035c5e2fa13)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/d08a6455-de18-428a-beed-9b8f0ebc691f)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/449cb31f-39d3-4c29-9c20-0833500720e2)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/fb537c03-8fb1-4f84-bb86-d0fdc90bea6b)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/856d71c6-86e9-4bfc-bd97-051c1ec0c655)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/b361c6f7-f222-47e5-bb5f-4b8184528e3b)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/dcc24b56-f21e-455e-be02-6ea91909810d)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/abe51a8f-3b83-43a6-9308-dba252dd2655)










Congratulations! You have successfully installed Kyverno on managed cluster using Red Hat Advanced Cluster Management.

