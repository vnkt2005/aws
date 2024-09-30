# AWS CodePipeline Hands-on
Pre-requisite: Git
1. Create an IAM policy for code pipeline.<br>
   - IAM-->Users-->Click on the existing user name -->Permissions -->Add Permission -->AWS CodeBuildAdminAccess<br>
   - SecurityCredentials --> HttpGitCredentialsFor AWS CodeCommit --> Generate Credentials --> Download Credentials --> Save it on local machine <br>

2. Create repository on CodeCommit.<br>
   This repository serves as source code for AWS CodePipeline <br>
   - CodeCommit --> Repository --> Create Repository --> Name: SampleWebApp --> Create <br>
   - For cloning this repository to local machine click --> Clone URL <br>

3. Create a sample folder on desktop of local machine.<br>
   - cd sample <br>
   - git clone http:// ...<br>
   - Provide username and pwd for Git Credential Manager <br>
   - cd SampleWebApp<br>
   - git status<br>
   - Now you can see the contents of Webapplication<br>
   - git add -A<br>
   - git commit -m "uploading"<br>

4. Push code to the code repository of the codecommit.<br>
   - push <br>

5. Goto CodeCommit Repository.<br>
   - You can view the source code here<br>

6. Create an EC2 Instance <br>
    - Name: CodePipelineInstance<br>
    - Choose AMI Linux<br>
    - Instance Type: t2.micro
    - Select key pair
    - Advanced Details --> user data -->
   ```sh
      #!/bin/bash
      yum -y update
      yum install -y ruby
      yum install -y aws-cli
      cd /home/ec2-user
      aws s3 cp s3://aws-codedeploy-us-east-1/latest/install --region us-east-1
      chmod +x ./install
      ./install auto
   ```

7. CodeDeploy
