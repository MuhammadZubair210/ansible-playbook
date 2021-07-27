Script to Create the Initial Inventory File

echo "[all]" > inventory

Script to Query EC2 for Instances and Output to File

aws ec2 describe-instances \
   --query 'Reservations[*].Instances[*].PublicIpAddress' \
   --output text >> inventory

Here, we called the output file inventory. But you could call it anything at all as long as you use the same name when running your Ansible Playbook later on.

Also, in the first script, we use > because we are creating a new file. Then, in the second script, we are using >> because we want to append the output to the file, not overwrite it (since it has our [all] header).
