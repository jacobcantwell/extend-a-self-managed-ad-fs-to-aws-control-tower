# Extend a self-managed Active Directory Federation Services to AWS Control Tower

(This blog entry is actively under development in a pre-alpha state)

One common use case for customers during their cloud journey is to use an existing identity service such as Microsoft Active Directory Federation Services.

In this blog post, I show you how to setup [AWS Control Tower](https://aws.amazon.com/controltower/) to delegate user authentication to a self-managed Microsoft Active Directory via AWS Managed Microsoft AD. This blog post shows a simulated environment on how to connect your existing on-premises Active Directory Federation Services to AWS Control Tower.

## Background

[AWS Single Sign-On (AWS SSO)](https://docs.aws.amazon.com/singlesignon/index.html) is a cloud service that enables you to manage SSO access to your AWS accounts, resources, and cloud applications centrally, for users from your preferred identity source.

When you enable AWS SSO, you allow it to create IAM roles for each AWS account in your AWS organization. You also allow other AWS accounts within your organization to assign applications access to AWS SSO users. (from products page)

Your identity source is the place where you administer and authenticate identities. You use AWS SSO to manage permissions for identities from your identity source to access AWS accounts, roles, and applications. AWS has three main identity sources: AWS SSO; Active Directory (AWS hosted or on-premise), or external SAML 2.0-compatible identity provider (IdP) such as [Octka](https://www.okta.com/products/single-sign-on/), [Azure AD][https://azure.microsoft.com/en-au/services/active-directory/], [Ping](https://www.pingidentity.com/en/software/pingfederate.html), or [OneLogin](https://www.onelogin.com/product/sso).

AWS Control Tower helps you automate the process of setting up a multi-account AWS environment [AWS Landing Zone](https://aws.amazon.com/solutions/implementations/aws-landing-zone/) that is secure, well-architected, and ready to use. This Landing Zone is created following best practices established through AWS’ experience working with thousands of enterprises as they move to the cloud. This includes the configuration of [AWS Organizations](https://aws.amazon.com/organizations/), centralized logging, federated access, mandatory guardrails, and networking.

AWS Control Tower incorporates AWS SSO, a cloud-based service that simplifies SSO access in a multi-account environment. Using AWS SSO, the directory connected to AWS Control Tower controls user authentication. Each user’s assigned account access and level of access permissions granted determines authorization.

You can use AWS Service Catalog apis to automate the creation of accounts in AWS Control Tower. With programmatic account creation using AWS Control Tower, you can create accounts in batches, apply customizations and verify account configuration.

## Limitations of Integrating with ADFS

* Creation of IAM Roles in each AWS Member account. AWS SSO does this centrally through Permission Sets.
* Creation of IAM IdPs. AWS SSO does this automatically when you push your first Permission Set to an account.
* AWS SSO provides a means to easily maintain configuration drift of IAM Roles. It does this by enabling an AWS SSO admin to push roles changes from the Main/Admin AWS account down to each Member account that the Permission Set is present in.
* ~~Certificate expiration~~

Permission Sets are JSON templates that tell AWS SSO how you want an IAM Role to look. You create these, assign user/group access to it, and then choose what AWS accounts will have it. AWS SSO the creates an IAM Role in that chosen AWS account, with the JSON policy in the Permission Set.

## Alternative Options

### SAML based authentication and SCIM based user/group automated provisioning 

You can use AWS Single Sign-On (AWS SSO) to authenticate identities from external identity providers (IdPs) through the Security Assertion Markup Language (SAML) 2.0 standard. This enables your users to sign in to the AWS SSO user portal with their corporate credentials. They can then navigate to their assigned accounts, roles, and applications hosted in external identity providers.





## Step # - Configure AWS SSO to use Azure Active Directory Federation Services as an External Identity Provider

AWS SSO works as a SAML 2.0 compliant service provider to your external identity provider (IdP). To configure your IdP as your AWS SSO identity source, you must establish a SAML trust relationship by exchanging meta data between your IdP and AWS SSO. While AWS SSO will use your IdP to authenticate users, the users must first be provisioned into AWS SSO before you can assign permissions to AWS accounts and resources.

* Log in to your AWS Control Tower Master account with Control Tower Administrator access.
* Enable AWS SSO in your master AWS account.
* On the AWS SSO Dashboard click the Choose your identity source link.
* In the Identity Source section, in the row Identity Source, click the Change link.
* Select External Identity Provider
* In the Service provider metadata section click Download metadata file and save on your computer as aws-sp.xml.
* Leave this browser tab open, and open a new tab to access your Microsoft Azure Console







## Resources

| Link | Summary |
| -- | -- |
| [A Self-Directed Journey to AWS Identity Federation Mastery](https://identity-federation.awssecworkshops.com/)| AWS workshops |
| [Control Tower Workshops](https://controltower.aws-management.tools/)| AWS Control Tower Immersion / Activation Day |
| [Enabling Federation to AWS Using Windows Active Directory, ADFS, and SAML 2.0](https://aws.amazon.com/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/)| |
| [How to Set Up SSO to the AWS Management Console for Multiple Accounts by Using AD FS and SAML 2.0](https://aws.amazon.com/blogs/security/how-to-set-up-sso-to-the-aws-management-console-for-multiple-accounts-by-using-ad-fs-and-saml-2-0/)| |
| [AWS Federated Authentication with Active Directory Federation Services (AD FS)](https://aws.amazon.com/blogs/security/aws-federated-authentication-with-active-directory-federation-services-ad-fs/)| |
| [How to Establish Federated Access to Your AWS Resources by Using Active Directory User Attributes](https://aws.amazon.com/blogs/security/how-to-establish-federated-access-to-your-aws-resources-by-using-active-directory-user-attributes/)| |
| ~~[How to automate SAML federation to multiple AWS accounts from Microsoft Azure Active Directory](https://aws.amazon.com/blogs/security/how-to-automate-saml-federation-to-multiple-aws-accounts-from-microsoft-azure-active-directory/)~~| |
| [Extend a self-managed Active Directory to AWS Control Tower](https://aws.amazon.com/blogs/mt/extend-a-self-managed-active-directory-to-aws-control-tower/)| |
| [The Next Evolution in AWS Single Sign-On](https://aws.amazon.com/blogs/aws/the-next-evolution-in-aws-single-sign-on/)| AWS SSO announcement |
| [Field Notes: Customizing the AWS Control Tower Account Factory with AWS Service Catalog](https://aws.amazon.com/blogs/architecture/field-notes-customizing-the-aws-control-tower-account-factory-with-aws-service-catalog/)| |
| [Programmatically Create an AWS Account with AWS Control Tower](https://www.youtube.com/watch?v=t0gxOsByOlA) | Create accounts in batches, apply customizations and verify account configuration. |


