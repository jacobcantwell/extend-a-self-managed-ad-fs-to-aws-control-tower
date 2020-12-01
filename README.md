# Extend a self-managed Active Directory Federation Services to AWS Control Tower

One common use case for customers during the early cloud journey is to use existing identity service such as Microsoft Active Directory Federation Services. In this blog post, I show you how to setup [AWS Control Tower](https://aws.amazon.com/controltower/) to delegate user authentication to a self-managed Microsoft Active Directory via AWS Managed Microsoft AD. This blog post shows a simulated environment on how to connect your existing on-premises Active Directory Federation Services to AWS Control Tower.

## Background

AWS Control Tower incorporates AWS Single Sign-on (AWS SSO), a cloud-based service that simplifies SSO access in a multi-account environment. Using AWS SSO, the directory connected to AWS Control Tower controls user authentication. Each user’s assigned account access and level of access permissions granted determines authorization.


