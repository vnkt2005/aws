# AWS CodePipeline Hands-on
Pre-requisite: Git
1. Create an IAM policy for code pipeline.<br>
   - IAM-->Users-->Click on the existing user name -->Permissions -->Add Permission -->AWS CodeBuildAdminAccess<br>
   - SecurityCredentials --> HttpGitCredentialsFor AWS CodeCommit --> Generate Credentials --> Download Credentials --> Save it on local machine <br>

2. Create repository on CodeCommit.<br>
   This repository serves as source code for AWS CodePipeline <br>
   - CodeCommit --> Repository --> Create Repository --> Name: SampleWebApp --> Create <br>
   - For cloning this repository to local machine click --> Clone URL <br>

