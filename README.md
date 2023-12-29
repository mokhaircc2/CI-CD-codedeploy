# CI-CD-codedeploy CI/CD using GitHub and AWS CodeDeploy*


<b>User Data for Dependencies installations for AMAZON Linux 2:-</b>

#!/bin/bash<br />

yum update -y yum<br />
install httpd -y<br />
systemctl start httpd<br />
systemctl enable httpd<br />
sudo yum -y install ruby<br />
sudo yum -y install wget<br />
cd /home/ec2-user<br />
wget  https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install<br />
sudo chmod +x ./install<br />
sudo ./install auto<br />
sudo yum install -y python-pip<br />
sudo pip install awscli<br />


In this project I created a multi-environment pipeline to deploy applications to a Dev and Prod environment using EC2 instances, CodeDeploy, CodePipeline and GitHub. I will be using Visual Studio Code to push any updates locally to our remote repository.

Launch 2 instances (Amazon Linux2, t2.micro), name them Dev and Prod and attach instance profile (role for CodeDeploy) to EC2. On the User data script configure the installation of Apache and CodeDeploy agent:

#!/bin/bash/

#install Apache
yum update -y yum<br />
install httpd -y<br />
systemctl start httpd<br />
systemctl enable httpd<br />

#install CodeDeploy agent yum install ruby -y yum install wget -y<br />

#wget https://bucket-name.s3.region-identifier.amazonaws.com/latest/install, bucket-name is the name of the Amazon S3 bucket that contains the CodeDeploy Resource Kit files for your region, and region-identifier is the identifier for your region. For a list of bucket names and region identifiers see Resource kit bucket names by Region on the AWS documentation.<br />

wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install<br />

#To execute permissions on the install file: chmod +x ./install<br />

#To install the latest version of the CodeDeploy agent: ./install auto<br />

#Using the public DNS name of the EC2 instance you can view its private IP address echo “This instance is: $(hostname) > /var/www/html/index.html<br />

If your application uses the EC2 compute platform, the AppSpec file must be a YAML-formatted file named appspec.yml and it must be placed in the root of the directory structure of an application's source code. Otherwise, deployments fail. It is used by CodeDeploy to determine:<br />

What it should install onto your instances from your application revision in Amazon S3 or GitHub.<br />
