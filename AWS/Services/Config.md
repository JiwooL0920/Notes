- fully managed service that provides you with an AWS resource inventory, config history, and config change notifications to enable security and governance
- multi-account/region data aggregation gives you an enterprise-wide view of your `Config Rule` compliance status, and associate your AWS organizations to quickly add your accounts
- Provides you pre-built rules to evaluate your AWS resource config and config changes, or create your own custom rules in Lambda that define internal best practices and guidelines for resource config
- `Config records`: details of changes to your AWS resources to provide you with a config history, and automatically deliver it to S3 bucket you specify
- Receive a notification whenever a resource is created/modified/deleted
- cloud/on-premise visibility into:
	- OS config
	- system level config
	- installed apps
	- network config
- Config deletes data older than your specified retention period. Default = 7 yrs

| Concepts                 | Definition                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Configuration History`  | A collection of config items for a given resource over any time period. Config automatically delivers a config history file for each resource type being recorded to S3 bucket you specify. A config history file is sent every 6 hrs for each resource type that it is recording                                                                                                       |
| `Configuration item`     | A record of configuration of a resource in your AWS account. Config creates a configuration item whenever it detects a change to a resource type that it's recording. Components include `metadata`, `attributes`, `relationships`, `current configuration`, and `related events`                                                                                                       |
| `Configuration Recorder` | Stores the configurations of supported resources in your account as configuration items. By default records all supported resources in the region where Config is running. Can create customized config recorder that record types you specify. You can also have Config record supported types of `global resources` which are IAM users, groups, roles, and customer managed policies |
| `Configuration Snapshot` | A complete picture of the resources that are being recorded and their configurations. Stored in S3 bucket that you specify                                                                                                                                                                                                                                                              |
| `Configuration Stream`   | An automatically updated list of all config items for the resources that Config is recording. Helpful for observing config changes as they occur so that you can spot potential problems, generating notifications if certain resources are changed, or updating external systems that need to reflect the config of your AWS resources                                                 |
| `Resource Relationship`  | Config discovers AWS resources in your account and then creates a map of relationship between AWS resources                                                                                                                                                                                                                                                                             |
| `Config Rule`            | Represents your desired config settings for specific AWS resources or for an entire AWS account. Provides customizable, predefined rules. If a resource violates a rule, Config flags the resource and the rule as noncompliant, and notifies you through SNS. Evaluates your resources either in response to config changes or periodically                                            |
| `Conformance Packs`      | A collection of rules and remediation actions. Created using YAML template with a list of managed/custom rules and remediation actions. Process checks enable you to list compliance of requirements and actions at a single location                                                                                                                                                   |
| `Config Aggregator`      | Collects config and compliance data from multiple accounts/regions, or in an Organization and all accounts in that org                                                                                                                                                                                                                                                                  |

# Config Monitoring
- Use **SNS** to send notifications everytime a supported AWS resource is created/updated/modified as a result of user API activity
- Use **CloudWatch Events** to detect/react to changes in the status of Config events
- Use **CloudTrail** to capture API calls to Config

# Config Security
- Use IAM to create individual users for anyone who needs access to Config and grant diff permissions to each IAM user
