# Commvault AWS Permissions

## Overview
JSON files for Amazon Web Services (AWS) IAM user permissions are present in this repository for performing certain cloud operations with Commvault.

The following backup solutions are supported by the Commvault platform and the required permissions are covered in this package:

| File                                         | Purpose                                                                                        |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| amazon_permission_backup_restore             | Protect Amazon Compute Cloud (EC2) instances                                                   |
| amazon_restricted_role_permissions           | Protect EC2 instances with delete access restricted to resources that are created by Commvault |
| amazon_documentdb_backup_restore_permissions | Protect Amazon DocumentDB clusters across multiple accounts and regions                        |
| amazon_rds_backup_restore_permissions        | Protect the Amazon RDS databases                                                               |
| amazon_redshift_backup_restore_permissions   | Protect Amazon Redshift clusters                                                               |
| amazon_DB_FS_permissions                     | Protect Amazon File system and application agents                                              |
| amazon_s3                                    | Perform backups to an S3 library                                                               |
| amazon_permission_conversion                 | Convert virtual machines to Amazon instances                                                   |
| amazon_vmimport_role_policy                  | Permissions for vmimport role                                                                  |
| amazon_vmimport_trust_policy                 | Trust policy for vmimport role                                                                 |

Prior to any conversion operations that use the import method, you must enable the VM Import Service role (vmimport) on the Amazon Web Services account and associate that role to the user account that is used to perform conversion operations.  

## Creating a vmimport role:
```
# From the AWS command line, use the create-role command to create a role named vmimport and to give VM import and VM export operations access to the role. Specify the full path to the location of the amazon_vmimport_trust_policy.json file, and add file:// before the path (for example, file://C:\trust-policy.json as shown in the following command):  
aws iam create-role --role-name vmimport --assume-role-policy-document file://C:\amazon_vmimport_trust_policy.json
# From the AWS command line, use the put-role-policy command to attach the policy to the vmimport role. Specify the full path to the location of the amazon_vmimport_role_policy.json file.  
aws iam put-role-policy --role-name vmimport --policy-name vmimport --policy-document file://C:\amazon_vmimport_role_policy.json
```

## Procedure to use the JSON file:  
1. Download the required json policy file.  
2. Create a IAM policy with the downloaded json  
3. Assign the policy to an IAM user or IAM role that is used for authentication of the Amazon hypervisor (Commvault virtualization client).  

For more information about IAM policies, see Overview of IAM Policies on the [AWS documentation site (https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html).  
 
