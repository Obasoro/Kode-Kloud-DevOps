## Task
```
1. Install jenkins on jenkins server using yum utility only, and start its service. You might face timeout issue while starting the Jenkins service, please refer this link for help.


2. Jenkin's admin user name should be theadmin, password should be Adm!n321, full name should be Jim and email should be jim@jenkins.stratos.xfusioncorp.com.


Note:


1. For this task, access the Jenkins server by SSH using the root user and password S3curePass from the jump host.


2. After Jenkins server installation, click the Jenkins button on the top bar to access the Jenkins UI and follow on-screen instructions to create an admin user.```

### Solution
[-]  Install jenkins on jenkins server using yum utility only, and start its service. You might face timeout issue while starting the Jenkins service, please refer this link for help.

```
ssh root@jenkins

password: S3curePass

yum install wget

[jenkins-installation-redhat](https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos)



