# Exercise #6: Deploy Kyverno Policies with ACM Policy

# Objective
Deploy and test a Kyverno policy using ACM on a remote cluster using ACM Policies

## Explainer
As shown in Exercise 5, we've encapsulated Kyverno Application installation inside ACM Policys so ACM will install the Application on itself and then on the remote clusters.
We are going to use the same method here, but now instead of encapsulate the entire kyvenro application, we are going to encapsulate only the Kyverno policy yaml in a ACM policy, that ACM will deploy on our chosen clusters based on specific label that we will add to the remote clusters. 

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/f50b22df-c4b5-4b8e-a2fd-1f162073afde)

# Prerequisites
1. Exercise 5
2. Helm

## Steps
**1. Examin one of the policies in the helm chart and explain what you see to the instructor**
```bash
cd /path/to/Ex6/dir
cd acm-kyverno-policies
less templates/policy-kyverno-config-exclude-resources-audit.yaml
```

**2. Go to the files directory and see the kyverno policy**
```bash
less files/disallow-latest-tag-audit.yaml
```

**3. Run the `helm template` command with one of the values file and see the results**
```bash
helm template . -f dev-values.yaml
```

**4. Run the same command with the second values file**
```bash
helm template . -f prod-values.yaml
```

**5. Explain to the instructor what is the difference between the two outcomes**

**6. While logged in to ACM, install the helm chart with the two values**
```bash
helm install dev-benchmark . -f dev-values.yaml -n kyverno
helm install prod-benchmark . -f prod-values.yaml  -n kyverno
helm list -n kyverno
```

**7. Tag the local cluster with the label of the dev-benchmark and see the results**


---

# Congratulations! You have successfully finished the workshop!
