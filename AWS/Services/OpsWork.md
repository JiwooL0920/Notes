- Configuration management service that helps you configure/operate apps in a cloud enterprise by using **Puppet** or **Chef**
	- `Puppet`: lets you configure a Puppet Enterprise master server in AWS
	- `Chef`: let you use Chef cookbooks and solutions for configuration management
- You can automate how nodes are configured, deployed, and managed, whether they're EC2 instances or on-premise devices

# OpsWork for Puppet Enterprise
- provides a fully-managed Puppet master, a suite of automation tools that enable you to inspect, deliver, operate, and future-proof your apps, and access to a user interface that lets you view info about your nodes and Puppet activities
- Doesn't support all regions
- Features
	- Retain control over underlying resources running your Puppet master
	- choose weekly maintenance window during with OpsWork for Puppet Enterprise will automatically install updates
	- Monitors the health of your Puppet master during update windows and auto roll back changes if issues are detected
	- configure backups for your Puppet master and store them in S3 bucket in your account
	- register new nodes to your Puppet master by inserting a user-data script, provided in the OpsWork for Puppet Enterprise StarterKit, into your ASG
	- Puppet use SSL and a certification approval process when communicating to ensure that the Puppet master responds only to requests made by trusted users
- Deleting a server also deletes its events, logs, and any modules that were stored on the server. Supporting resources are also deleted, along with all automated backups
- Charged based on the number of nodes (servers running Puppet agent) connected to your Puppet master and the time those nodes are running on an hourly rate. + underlying EC2 instance running Puppet master