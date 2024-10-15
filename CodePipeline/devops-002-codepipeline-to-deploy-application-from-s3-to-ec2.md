# To deploy an application from AWS S3 to AWS EC2 Instance
1. Create AWSCodeDeployRole<br>
  IAM --> Roles --> Create role --> Use case: CodeDeploy --> Next --><br>
  Policy already attached --> next --> role name: mydemocodedeployrole --> create role <br><br>
2. Create AmazonEC2RoleForAWSCodeDeploy<br>
  IAM --> Roles --> Create role --> Use case: EC2 --> Next --> <br>
  Policy name: AmazonEC2RoleforAWSCodeDeploy --> Attach it by clicking on tick mark --> Next <br>
  Role name: mydemoec2role --> create role<br><br>
3. Create an S3 bucket for your application<br>
  Source Code: index.html<br>
  S3 --> Create Bucket --> bucket name: mydemo --> bucket versioning: enable --> create bucket<br>
  click on mydemo --> drag and drop index.html from laptop on to mydemo bucket --> upload<br><br>
4. Create EC2 Linux instance and install CodeDeploy agent<br>
  EC2 --> Launch Instance --> Amazon Linux --> t2 micro --> Enable: Auto assign public IP --> <br>
  IAM Role: mydemoec2role --> user data: copy as shown below --> expand the user data box and clear if any spaces<br>
  Next --> Add tags: Key: Name, Value: My first ec2 instance --> <br>
  Security group: Add Rule --> HTTP, Anywhere --> Review and Launch <br>
  Select a key pair if required and acknowledge<br>
<br>
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
  CodeDeploy --> application --> Application name: mydemoapp --> <br>
  compute platform: EC2/On-premises --> create application <br>
    <br>
  - Create Deployment Group<br>
  Create deployment group --> group name: mydemodeploymentgroup --> <br>
  service role: mydemocodedeployrole --> Environment configuration : Amazon EC2 instance <br>
  Key: Name, Value: My first instance --> Load balance: disable --> <br>
  create deployment group
    <br>
6. Create Pipeline<br>
  Pipelines --> create pipeline --> pipeline name: mydemopipeline (without any spaces) --> <br>
  service role: new service role --> check: allow to create service role --> <br>
  next --> source provider: Amazon S3 --> bucket: mydemo --> s3 object key: index.html <br>
  next --> skip build stage --> deploy: AWS code deploy --> application name: mydemo <br>
  deployment group: mydemogroup --> create pipeline <br>
  <br>
7. Verify deployment<br>
  goto EC2 instance --> copy public IP --> paste on google chrome --> view website <br>
  <br>
8. Cleanup Resources<br>
  <br>
  

