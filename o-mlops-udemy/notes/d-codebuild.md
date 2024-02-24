## CodeBuild

* Create a CodeCommit Git repo for this purpose.
```sh
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ git init
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codebuild-repo
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ git add .
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ git commit -m "Version1"
[master (root-commit) 80922ad] Version1
 11 files changed, 315 insertions(+)
 create mode 100644 CODEDEPLOY.md
 create mode 100644 HELP.md
 create mode 100644 appspec.yml
 create mode 100644 buildspec.yml
 create mode 100644 code.py
 create mode 100644 index.html
 create mode 100644 scripts/after_install.sh
 create mode 100644 scripts/install_dependencies.sh
 create mode 100644 scripts/start_server.sh
 create mode 100644 scripts/stop_server.sh
 create mode 100644 scripts/validate_service.sh
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ git push -u origin master
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 12 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (14/14), 4.33 KiB | 4.33 MiB/s, done.
Total 14 (delta 0), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codebuild-repo
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
(torch-env) (base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/codebuild-repo$ 


```

buildspec.yml file

```sh
version: 0.2

env:
    variables:
        MY_AWS_REGION: "ap-south-1"


phases: 
    install:
        runtime-versions:
            nodejs: 12
        commands:
            - echo "Running on $MY_AWS_REGION"
            - echo "Print Environment Variables"
            - printenv
            - echo "Start the installation process"
            - echo "Installation Process Completed"
    pre_build:
        commands: 
            - echo "This is the start of Pre-Build phase"
            - echo "Pre-Build phase is now completed"
    build:
        commands:
            - echo "we are currently on build phase"
            - echo "Build Activity is completed"
            - echo "Run Basic check whether Website is ready for use"
            - grep -Fq "AWS Certified DevOps Engineer" index.html
            - echo "Test was successful"
            - echo "proceed with next steps"
    post_build:
        commands:
            - echo "We are currently on post_build phase"
            - echo "post_build phase activity is completed. Moving next to Artifacts"

artifacts:
    files:
    - '**/*'



```


* In order to save artifacts, enable that in UI, pass the S3. and then add that in buildspec.yaml.

* Now we need to automate the build, instead of manual.. 
* Use AWS EventBridge > Rules > create >
select aws services and use codecommit, and pick whatever event you want.
* then select target as codebuild project and mention ARN.

