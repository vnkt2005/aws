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

7. CodeDeploy<br>
  - CodeDeploy --> Applications --> Create application --> ApplicationName: SampleApp <br>
  - --> ComputePlatform: EC2/On-Premises --Create Application

8. Create Deployment Group<br>
  - Click on CreateDeploymentGroup --> GroupName: SampleGroup <br>
  - Enter a service role: select a role --> Deployment type: in-place <br>
  - Environment configuration: Amazon EC2 instances --> Key: Name, Value: CodePipelineInstance<br>
  - Uncheck: Load balancing --> Create deployment group <br>

9. Create code pipeline<br>
  - Pipelines --> Create pipeline --> pipeline name: samplepipeline --><br>
  - Next --> Source provider: select AWS CodeCommit --> Repository Name: SampleWebApp --><br>
  - Branch: master --> Next --> Skip Build Stage --> <br>
  - Deploy Provider: AWS CodeDeploy --> Region: choose --> <br>
  - Application Name: SampleApp --> Deployment Group: Sample Group --> Review --><br>
  - Create Pipeline --> source stage --> deploy stage --> should be successful<br>

10. Verify deployment on EC2 instance<br>
  - Go to EC2 instance --> Public IPv Address --> Copy --> Paste it in a browser <br>
  - See your application successfully deployed.


# Troubleshooting while git clone
```sh
Fix aws codecommit unable to access repository (The requested URL returned error: 403) in windows
this was tested using windows10 pro

when cloning a git this error was produced
fatal: unable to access 'https://git-codecommit.us-east-1.amazonaws.com/v1/repos/RepositoryName': The requested URL returned error: 403

to fix add the following git configuration
git config --global credential.helper "!aws codecommit credential-helper $@"
git config --global credential.UseHttpPath true

check if git has system credential.helper by typing 
git config --system -l

if it has remove it by typing
git config --system --unset credential.helper
```

