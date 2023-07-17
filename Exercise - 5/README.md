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

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/3578410e-7aa5-4721-bc3a-20c08bbe116a)

## Kyverno & ACM Integration
In order to deploy and manage the Kyverno application life-cycle using helm charts, we will “orchestrate” the local and remote deployment of Kyverno on top of our clusters; we will be using ACM and its application deployment mechanism.

You will need to create the following  5 YAML’s:
* Namespace — which will be created on the remote cluster and in which our ACM policy is going to be deployed
* Channel — Points to the Git Repo where the chart resides
* PlacementRule — Let ACM know on which clusters the application should be deployed onto. 
> In the exercise we will create a dedicated PlacementRule that will tell ACM to deploy Kyverno on "install-kyverno=true" labeled clusters.
* Subscription — Link between the channel and the placementRule and allow us to override some values of the helm chart if needed without editing the one in the repository
* Application — Points to the subscription

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/eff43b1e-f92b-4cba-b7fc-a5af36e9e1ae)

> Note! In our demo environment we are using a single Openshift cluster per-student that will function both as ACM Hub cluster and as the managed cluster that we will install Kyverno on. 
> You can see the following [recorded demo](https://www.youtube.com/watch?v=2RkVDzvBN6w) that demonstrates how to import a remote cluster to be managed by RHACM

> Also Note! In this exercise we are using a uniqe method of deploying ACM Application on ACM Hub using ACM Governance Policy mechanisem. We are doing this because of a CRD that Kyverno requiers that we cannot edit with the regular Application Lifecycle of RHACM, and it also keeps all of our yamls in a single file in an organized manner.
> ![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/714f3f01-c2df-4ad8-8f66-d810aa899a87)
> ![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/3b5e003a-200e-4fe2-a6c0-b836864c9c6d)




## Prerequisites
- A running Kubernetes/Openshift cluster with at least 3 master nodes
- Helm v3 or later installed on your local machine
- ACM Hub installed on the Openshift Cluster (Part 1 of this exercise)

## Steps
1. **Delete any old Kyverno installed on the cluster from the previous exercises**
```bash
oc login <OCP Cluster>
helm list --all-namespaces | grep kyverno
helm uninstall kyvenro -n kyverno
```
   
2. **Install RHACM on the cluster** (Done in Part 1)
3. **Switch to ACM view from the Openshift Web UI**

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/aa5b80f4-e6c3-47d3-914f-abe56d9ef74b)
![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/4d200df9-6ce0-4d7b-b14c-58e6520dc1f1)

4. **Go over the following YAML with the instractor**
```bash
cd /PATH/to/Exercise 5
cat policy-install-kyverno.yaml
oc apply -f policy-install-kyverno.yaml
```

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/ce623ae1-5f37-44f8-87e7-5cffc26f58b8)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/e0bc98d8-9d18-4bf5-929d-57cce13b4c87)


5. **Label the local cluster with the label "install-kyverno=true" and see the application is being installed on it by ACM in the appication view**

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/dfe4096e-c70e-4b41-9a72-5035c5e2fa13)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/d08a6455-de18-428a-beed-9b8f0ebc691f)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/449cb31f-39d3-4c29-9c20-0833500720e2)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/fb537c03-8fb1-4f84-bb86-d0fdc90bea6b)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/856d71c6-86e9-4bfc-bd97-051c1ec0c655)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/b361c6f7-f222-47e5-bb5f-4b8184528e3b)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/dcc24b56-f21e-455e-be02-6ea91909810d)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/abe51a8f-3b83-43a6-9308-dba252dd2655)

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/65958f7d-591d-4846-93cc-23b50bb7df18)



You can also see the entire process in the following [article](https://medium.com/@tamber/howto-deploy-custom-made-helm-charts-on-multi-openshift-clusters-w-advanced-cluster-management-9f34942bb0b4)







Congratulations! You have successfully installed Kyverno on managed cluster using Red Hat Advanced Cluster Management.

