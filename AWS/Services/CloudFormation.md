- Easy way to create a collection of related AWS resources and provision them
- model your entire infra as `template`
- you can use `Rollback Triggers` to specify **CloudWatch alarm** that CF should monitor during stack creation/update process
- `CloudFormation Change Sets`: allow you to preview how proposed changes to a stack might impact your running resources
- `Stack Sets`: automatic/safe provisioning, updating, or deleting stacks (common set of AWS resources) across **multiple accounts/regions** with a single CF template
- Build `custom extensions` to your stack template using **Lambda**
-  `CloudFormation Registry` helps you discover/provision private/public extensions such as resources, modules, and hooks in your CloudFormation templates
- `CloudFormation Artifacts`: can include
	- `Stack Template File`: defines the resources that CF provisions and configures (YAML/JSON)
	- `Template Configuration File`: JSON-formatted text file that can specify template parameter values, a stack policy, and tags
- Though **PrivateLink**, you can use CF APIs inside your VPC and route data between your VPC and CloudFormation entirely within AWS network

| CloudFormation                                            | Elastic BeanStalk                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------------ |
| Provisioning mechanism for a broad range of AWS resources | Provides an environment to easily deploy and run apps in the cloud |

# Stacks
- if a resource can't be created, CF rolls the stack back and auto deletes any resources that were created. If a resource can't be deleted, any remaining resources are retained until the Stack can be successfully deleted
- Stack update methods
	- direct update
	- Creating and executing change sets
- When you update a stack, CF will only update resources that have been modified in the current stack template. And while the update is being applied, resources that haven't changed will continue to operate without any disruption
- `Drift Detection` enables you to detect whether a stack's actual config differs, or has drifted, from its expected config. Use CF to detect drift on an entire stack, or an individual resources within the stack
	- a **resource** is considered drifted if its actual property values differ from the expected value
	- a **stack** is considered drifted if one or more of its resources have drifted
- to share info between stacks, `export` a stack's output values. Other stacks that are in the **same AWS account and region** can `import` the exported values
- You can nest stacks and create Microsoft Windows stacks
- Using resource import, you can import/manage AWS resources that are created outside of CloudFormation. You can also move resources between stacks by adding a `Retain` deletion policy
- stack failure options allows you to troubleshoot resources in a `CREATED_FAIL` or `UPDATE_FAILED` status without rolling back successfully provisioned resources 

# Templates
- include several major sections -- the `Resources` section is the only required section
- `CloudFormation Designer` is a graphic tool for creating, viewing, and modifying CF templates
- `Custom resources` enable you to write custom provisioning logic in templates that CF runs anytime you create/update/delete stacks
- `Template macros` enable you to perform custom processing on templates (ex. find and replace, extensive transformations of entire templates)
- `Modules`: building blocks that can be reused across different CloudFormation templates
- You can use regular expressions when creating a template parameter
- You can use CF to perform ECS blue/green deployments via CodeDeploy

# StackSets
- `Stack sets:` Allow you to roll out CF stacks over multiple AWS accounts/regions using a single CF template. All resources included in each stack are defined by the stack set's CF template. It's a **regional** resource
- `Stack instance`: reference to a stack in a target account within a region. A stack instance can exist without a stack (ex. if the stack couldn't be created, the stack instance shows the reason for stack creation failure). A stack instance can be associated with only one stack set
- `Stack set operations`: create/update/delete, StackSets generates status codes
- `Stack set operations options`: max concurrent accounts, failure tolerance, retain stacks, and region concurrency
- `Tags`: you can add tags during stack set creation and update operations by specifying key/value pairs
- Commonly used together with **AWS Organizations** to centrally deploy/manage services in diff accounts
- `Administrator account`: the AWS account in which you create stack sets. A stack set is managed by singing into the admin account in which it was created
- `Target account`: the account into which you create, update, or delete one or more stacks in your stack set
- You can delegate other admin accounts in your AWS Organization that can create/manage stack sets with **service managed permissions** for the organization
- You can configure an account gate or Lambda function to verify a target account meets certain requirements before it begins stack operations
- Stack import operations:
	- `Self-managed Stacksets`: stacks can be imported into the admin account or into other target accounts/regions
	- `Service-managed StackSets`: any stack in the same AWS Organizations as the management account can be imported

# CloudFormation Monitoring
- integrated with **CloudTrail** -- captures all API calls for CF as events, including calls from CF console and CF API

# CloudFormation Security
- you can use **IAM** with CF to control what users can do
- A `service role` is an IAM role that allows CF to make calls to resources in a stack on your behalf. You can specify an IAM role that allows CF to create/update/delete your stack resuorces
- You can improve security posture of your VPC by configuring CF to use an **interface VPC endpoint**

# Pricing
- No additional charge for CF. Pay for AWS resources created using CF in the same manner as if you created them manually