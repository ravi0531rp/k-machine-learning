## Codedeploy

* Features
1) Fully Managed Deployment Service
2) Can use AWS EC2, Fargate, Lambda
3) Avoid Downtime
4) Provides Autoscaling
5) Rollback Support

* Benefits
1) Repeatable Deployments
2) Auto scaling
3) Centralized Control
4) Easy to Adopt
5) Use Appspec.yaml to automate everything

* Types of Deployments
1) In-place ==> Update the app on existing Instances
2) Blue Green ==> Gradually Replace Existing Instance with instance running new versions (Good for prod)



* Installing the CodeDeploy agent on EC2
```sh

- Create EC2 Instance with IAM Role attached
    - Assign the Policy `AmazonS3ReadOnlyAccess` to allow CodeDeploy agent to read the version from S3 Bucket
    - Add User Data as mentioned below
- Assign tags to EC2 Instances
- Launch the instance and run the command - `sudo service codedeploy-agent status` to validate - CodeDeploy Agent is not running in EC2 instance
- Create an Application in CodeDeploy
- Push app revision to S3 Bucket (create a S3 bucket with versioning if its not created) - see section - **deploy the files into S3** below
- Create a Service Role for CodeDeploy and assign Codedeploy policy
- Create CodeDeployment Group and assign IAM role created above
- Do necessary settings and create Code Deployment
- Run the Deployment
- Verify whether the website is working (Make sure to check the security group of ec2 instance)
```

* Manual Steps for CodeDeploy Agent
```sh
sudo yum update -y
sudo yum install -y ruby
sudo yum install -y wget
cd /home/ec2-user
wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent status

#If error
sudo service codedeploy-agent start
sudo service codedeploy-agent status
```

* User data for putting in EC2 user data while creating instances (Why use Manual lol)
```sh
#!bin/bash
sudo yum update -y
sudo yum install -y ruby wget
wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
sudo service codedeploy-agent status
```

* Create a bucket and enable versioning
```sh
## https://docs.aws.amazon.com/cli/latest/reference/s3/mb.html
## https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-versioning.html

aws s3 mb s3://aws-ravi-mlops --region us-east-1 
aws s3api put-bucket-versioning --bucket aws-ravi-mlops --versioning-configuration Status=Enabled --region us-east-1 
```

* Deploy the files into S3
```sh
# https://docs.aws.amazon.com/cli/latest/reference/deploy/push.html
aws deploy push --application-name demo-app --s3-location s3://aws-ravi-mlops/demo-app/app.zip --ignore-hidden-files --region us-east-1 
```

Output
```sh

(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ aws deploy push --application-name demo-app --s3-location s3://aws-ravi-mlops/demo-app/app.zip --ignore-hidden-files --region us-east-1 
To deploy with this revision, run:
aws deploy create-deployment --application-name demo-app --s3-location bucket=aws-ravi-mlops,key=demo-app/app.zip,bundleType=zip,eTag=fe781f7415612409f11a485978f34efc,version=pYb21mP7Rvu3f6WD9xr05__AETJn67dt --deployment-group-name <deployment-group-name> --deployment-config-name <deployment-config-name> --description <description>


```
* Now go to Codedeploy App, create a deployment group and add settings, attach service roles, EC2 
and everything like Deployment Strategy.. 

* Take a look at appspec.yaml file

```sh
version: 0.0
os: linux
files:
  - source: /index.html
    destination: /var/www/html/
hooks:
  ApplicationStop:
    - location: scripts/stop_server.sh
      timeout: 300
      runas: root

  BeforeInstall:
    - location: scripts/install_dependencies.sh
      timeout: 300
      runas: root

  AfterInstall:
    - location: scripts/after_install.sh
      timeout: 300
      runas: root

  ApplicationStart:
    - location: scripts/start_server.sh
      timeout: 300
      runas: root

  ValidateService:
    - location: scripts/validate_service.sh
      timeout: 300
  



```