

<!-- step-by-step instructions for setting up Amazon EC2 - application deployment -->

1) Search for “EC2” in the search bar at the top of your screen. Go to your Amazon EC2 dashboard and click the “Instance” menu on the left sidebar.

Then click the “Launch Instance” button to start setting up your server.


On the next screen, you can provide a descriptive name for your server. This name will be displayed in the AWS dashboard.

2). Choose Ubuntu Server Image
Next, you need to choose an Amazon Machine Image (AMI) for your instance (Amazon Linux or Ubuntu)

3). Choose Amazon EC2 Instance Type
Under the “Instance Type” option, select one of the predefined instance types for your instance. Each type has a certain number of vCPUs (virtual Central Processing Unit) and memory.
For example, you can choose the t2.micro instance with 1 vCPU and 1GB Memory that is free for AWS Free Tier users. Each instance type in different AWS region is priced differently. Refer to the AWS pricing chart for up to date information on this topic.

Create and Download a SSH Key
Next, you will need to specify the SSH key that you want to use to log into this server. If you already have an existing key-pair, you can either use that, or use the built-in utility to create a new key pair and save it to your local computer. You will not be able to download the file again after it’s created.


Configure Security Group (Open Required Ports)
Next, you need to open the required ports on your EC2 instance. This step is very important to make your Amazon EC2 instance reachable on the internet.

You need open the following 4 ports:
SSH – TCP Port 22
HTTP – TCP Port 80
HTTPS – TCP Port 443
Custom – TCP Port 34210

To add the above rules, click on “Edit” next to the “Network Settings” sub menu and fill in the following details:
Auto-assign public IP: Disable (we will assign a static IP in next step)

Firewall (security groups): Create New security Group
Security group name: runcloud-security-group
Description: RunCloud needs these ports to function properly




Next, you need to add the rules to open required TCP ports and allow connections from anywhere. For the SSH rule, we recommend setting the source type to “My IP“. This will block any connection requests that originate from outside your network.
You should note that most residential internet connections do not have a permanent IP address, which means that your IP address will change roughly every 24 hours. Due to this, if you try to log in to your server in future, your SSH connection will be blocked.
To fix this, you can just log back into your AWS account and edit the runcloud-security-group again to use your new IP.



Connect to Your Amazon EC2 Instance Using SSH
Go back to the Amazon EC2 dashboard and find your server under the Instances menu. Select the instance and click on the “Connect” button at the top.


On the next screen, switch to the “SSH Client” tab. There you will see the commands that you need to execute to connect to your server.



Open an SSH client and go to the directory where you saved the SSH key that you downloaded when creating the server. To verify that you are in the correct directory, you can run ls <key name> to see if the key is present in the current directory.
For example, if the name of your key is my-SSH-Key.pem, you will run ls my-SSH-Key.pem. If this shows you the name of your key, then you are in the right place. If you don’t get anything then you need to change the directory using cd command.
From this directory, run the following command to change the permissions of the SSH key:
chmod 400 <SSH Key name>.pem

Then, you can connect to the server via

ssh -I “<SSH Key name>.pem” ubuntu@<ip address to your server”





