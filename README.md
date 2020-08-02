## Prerequisites


### Ansible

* Installation of ansible and other required modules
```bash
pip3 install --user ansible boto3 boto
```

* Verification
```bash
which ansible
```
* Point the python interpreter in `inventory.ini` to the python version used by your pip installer. In above case, it is python3.7. You can get the details of the python version being used by pip through:

```bash
pip3 --version
```

OR 

```bash
pip --version
```

* Troubleshooting

If the ansible command is not found even after successful installation. Check system's Path variable if it consists python packages' location described in the output of the ansible installation command. If not, run below command to add the python bin location to your path variable in your bash profile file. 

```bash
echo 'export PATH="$HOME/Library/Python/3.7/bin:$PATH"' >>  ~/.bash_profile
source ~/.bash_profile
```

### AWS credentials

The ansible playbook needs AWS programmatic access for creating infra componentns. Hence, it requires AWS access key and secret key present under default profile in AWS creds file: `~/.aws/credentials` on your machine. You can create your AWS user and AWS access keys from AWS IAM console: https://console.aws.amazon.com/iam/home?region=us-east-1#/users

Sample aws cred file:

```
[default]
aws_access_key_id = <AWS_ACCESS_KEY_ID_CREATED_ON_AWS_CONSOLE>
aws_secret_access_key = <AWS_SECRET_ACCESS_KEY_CREATED_ON_AWS_CONSOLE>
```

## Running the playbook

```bash
ansible-playbook playbook.yml
```

Once, this playbook successfully gets executed, access the static HTML page on browser. The IP serving the request can be found at the end of ansible-playbook execution logs. 

## TODO

* If the ssh keys are compromised and one needs to rotate it. Existing instance would not be bounced. And the private key would be lost. Hence, the instances couldn't be sshed. 
* The nginx provisioning part can be done through ec2 instance's user data. The user data would run ansible in pull mode from github. This will remove coupling between infra provisioning and nginx provisioning. 
* Set up Route53 hosted zone for routing subdomain rather than using IP.  

