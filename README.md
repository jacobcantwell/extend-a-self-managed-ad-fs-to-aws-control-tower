# Extend a self-managed Active Directory Federation Services to AWS Control Tower

One common use case for customers during their cloud journey is to use an existing identity service such as Microsoft Active Directory Federation Services.

In this blog post, I show you how to setup [AWS Control Tower](https://aws.amazon.com/controltower/) to delegate user authentication to a self-managed Microsoft Active Directory via AWS Managed Microsoft AD. This blog post shows a simulated environment on how to connect your existing on-premises Active Directory Federation Services to AWS Control Tower.

## Background

[AWS Single Sign-On (AWS SSO)](https://docs.aws.amazon.com/singlesignon/index.html) is a cloud service that enables you to manage SSO access to your AWS accounts, resources, and cloud applications centrally, for users from your preferred identity source.

When you enable AWS SSO, you allow it to create IAM roles for each AWS account in your AWS organization. You also allow other AWS accounts within your organization to assign applications access to AWS SSO users. (from products page)

Your identity source is the place where you administer and authenticate identities. You use AWS SSO to manage permissions for identities from your identity source to access AWS accounts, roles, and applications. AWS has three main identity sources: AWS SSO; Active Directory (AWS hosted or on-premise), or external SAML 2.0-compatible identity provider (IdP) such as [Octka](https://www.okta.com/products/single-sign-on/), Azure AD, Ping, or OneLogin.

AWS Control Tower incorporates AWS SSO, a cloud-based service that simplifies SSO access in a multi-account environment. Using AWS SSO, the directory connected to AWS Control Tower controls user authentication. Each user’s assigned account access and level of access permissions granted determines authorization.

## Limitations of Integrating with ADFS

* Creation of IAM Roles in each AWS Member account. AWS SSO does this centrally through Permission Sets.
* Creation of IAM IdPs. AWS SSO does this automatically when you push your first Permission Set to an account.
* AWS SSO provides a means to easily maintain configuration drift of IAM Roles. It does this by enabling an AWS SSO admin to push roles changes from the Main/Admin AWS account down to each Member account that the Permission Set is present in.
* ~~Certificate expiration~~

Permission Sets are JSON templates that tell AWS SSO how you want an IAM Role to look. You create these, assign user/group access to it, and then choose what AWS accounts will have it. AWS SSO the creates an IAM Role in that chosen AWS account, with the JSON policy in the Permission Set.

## Alternative Options




## 

* AWS SSO is configured in a master AWS account.







## Resources

* [A Self-Directed Journey to AWS Identity Federation Mastery](https://identity-federation.awssecworkshops.com/)
* [Enabling Federation to AWS Using Windows Active Directory, ADFS, and SAML 2.0](https://aws.amazon.com/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/)
* [How to Set Up SSO to the AWS Management Console for Multiple Accounts by Using AD FS and SAML 2.0](https://aws.amazon.com/blogs/security/how-to-set-up-sso-to-the-aws-management-console-for-multiple-accounts-by-using-ad-fs-and-saml-2-0/)
* [How to Establish Federated Access to Your AWS Resources by Using Active Directory User Attributes](https://aws.amazon.com/blogs/security/how-to-establish-federated-access-to-your-aws-resources-by-using-active-directory-user-attributes/)
* [AWS Federated Authentication with Active Directory Federation Services (AD FS)](https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/)
* [Extend a self-managed Active Directory to AWS Control Tower](https://aws.amazon.com/blogs/mt/extend-a-self-managed-active-directory-to-aws-control-tower/)
