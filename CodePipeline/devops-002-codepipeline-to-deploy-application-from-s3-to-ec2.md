# To deploy an application from AWS S3 to AWS EC2 Instance
1. Create AWSCodeDeployRole<br>
  
2. Create AmazonEC2RoleForAWSCodeDeploy<br>
  IAM --> Roles --> Create role --> Use case: EC2 --> Next --> <br>
  Policy name: AmazonEC2RoleforAWSCodeDeploy --> Attach it by clicking on tick mark --> Next <br>
  Role name: mydemoec2role --> create role<br>
3. Create an S3 bucket for your application<br>
  Source Code: index.html<br>
  S3 --> Create Bucket --> bucket name: mydemo --> bucket versioning: enable --> create bucket<br>
  click on mydemo --> drag and drop index.html from laptop on to mydemo bucket --> upload<br>
4. Create EC2 Linux instance and install CodeDeploy agent<br>
  Role: AmazonEC2RoleForAWSCodeDeploy<br>
  User Data: <br>
  ```sh
  #!/bin/bash
  yum -y update
  yum install -y ruby
  yum install -y aws-cli
  cd /home/ec2-user
  wget https://aws-codedeploy-us-east-2.s3.us-east-2.amazonaws.com/latest/install
  chmod +x ./install
  ./install auto
  ```
5. Create application and deployment group<br>
  Role: AWSCodeDeployRole<br>
  - Create application<br>
  - Create Deployment Group<br>
6. Create Pipeline<br>
7. Verify deployment<br>
8. Cleanup Resources<br>
  

