# CI/CD using GitHub and AWS CodeDeploy

In this project I created a multi-environment pipeline to deploy applications to a Dev and Prod environment using EC2 instances, CodeDeploy, CodePipeline and GitHub. I will be using Visual Studio Code to push any updates locally to our remote repository.

Launch 2 instances (Amazon Linux2, t2.micro), name them Dev and Prod and attach instance profile (role for CodeDeploy) to EC2. On the User data script configure the installation of Apache and CodeDeploy agent:<br />

UserData script
<b>User Data for Dependencies installations for AMAZON Linux 2:-</b>
#!/bin/bash<br />

#install Apache<br />
yum update -y<br />
yum install httpd -y<br />
systemctl start httpd<br />
systemctl enable httpd<br />

#install CodeDeploy agent<br />
yum install ruby -y<br />
yum install wget -y<br />

#Amazon S3 bucket contains the CodeDeploy Resource Kit files for your region. For a list of bucket names and region identifiers see Resource kit bucket names by Region on the AWS documentation.<br />
wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install<br />

#To execute permissions on the install file:<br /> 
chmod +x ./install<br />

#To install the latest version of the CodeDeploy agent:<br />
./install auto<br />
