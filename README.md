### Running the script 

<hr />

### Script to Create the Initial Inventory File

``` sh
echo "[all]" > inventory
```

### Script to Query EC2 for Instances and Output to File

``` sh
$ aws ec2 describe-instances \
   --query 'Reservations[*].Instances[*].PublicIpAddress' \
   --output text >> inventory
```

### Things you should know

Here, we called the output file inventory. But you could call it anything at all as long as you use the same name when running your Ansible Playbook later on.

Also, in the first script, we use > because we are creating a new file. Then, in the second script, we are using >> because we want to append the output to the file, not overwrite it (since it has our [all] header).


Ansible Exercise

Exercise: Build Ansible Inventory File
We are going to generate an Ansible inventory file using the AWS CLI. So that we can easily reference devices and machines from our Ansible Playbook, we need to list those devices in an inventory file. Instead of creating it manually, we're going to use AWS to list the EC2 instance hostnames and then we will pipe that to an inventory file automatically.

Instructions:
Create an EC2 instance in your AWS account for testing (micro/free tier is fine). Add a memorable tag like Project:udacity to the instance. Please remember the tag name you're adding.
If you don't have AWS CLI installed and configured, please do that now.
Create a "starter" inventory file called inventory with which we're going to add the value of all using the bash command echo [all] > inventory.
Run the following CLI command to list the EC2 instances:
aws ec2 describe-instances \
\
        --query 'Reservations[*].Instances[*].PublicIpAddress' \
      --filters "Name=tag:Project,Values=udacity" \
      --output text >> inventory
This will append the "udacity" instance IP addresses to our inventory file and should look something like this:

[all]
169.254.123.12
XX.XXX.XXX.XX will be the public IP of your udacity-tagged instance.

Terminate any test EC2 instances you created for this exercise to clean up.

For Some Extra Challenge
Try wrapping this script in a Circle CI job and save the inventory file to the cache or workspace. You'll have to do this later in your project, but it might help to try it now to get a head start!

