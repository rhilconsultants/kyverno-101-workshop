# Exercise #6: Deploy Kyverno Policies with ACM Policy

# Objective
Deploy and test a Kyverno policy using ACM on a remote cluster using ACM Policies

## Explainer
As shown in Exercise 5, we've encapsulated Kyverno Application installation inside ACM Policys so ACM will install the Application on itself and then on the remote clusters.
We are going to use the same method here, but now instead of encapsulate the entire kyvenro application, we are going to encapsulate only the Kyverno policy yaml in a ACM policy, that ACM will deploy on our chosen clusters based on specific label that we will add to the remote clusters. 

![image](https://github.com/rhilconsultants/kyverno-101-workshop/assets/60185557/f50b22df-c4b5-4b8e-a2fd-1f162073afde)

# Prerequisites
1. Exercise 5 

## The policies we will test

  - **Policy #1**
    * **Name:** Disallow Latest Tag
    * **Type:** Validate
    * **Description:** The ':latest' tag is mutable and can lead to unexpected errors if the image changes. A best practice is to use an immutable tag that maps to a specific version of an application Pod. This policy validates that the image specifies a tag and that it is not called `latest`.
    * [Kyverno.io Link](https://kyverno.io/policies/best-practices/disallow-latest-tag/disallow-latest-tag/)
    * [GitHub Link](https://github.com/kyverno/policies/tree/main/best-practices/disallow-latest-tag)
    > Note! The GitHub link holds preconfigured testing YAMLs you can use
    * [GitHub raw Link](https://raw.githubusercontent.com/kyverno/policies/main/best-practices/disallow-latest-tag/disallow-latest-tag.yaml)

# Steps
