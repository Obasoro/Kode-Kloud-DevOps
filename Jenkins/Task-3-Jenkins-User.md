## task 3

---
Jenkins User

----


The Nautilus team is integrating Jenkins into their CI/CD pipelines. After setting up a new Jenkins server, they're now configuring user access for the development team, Follow these steps:



1. Click on the Jenkins button on the top bar to access the Jenkins UI. Login with username admin and password Adm!n321.

2. Create a jenkins user named john with the passwordksH85UJjhb. Their full name should match John.

<img width="1362" height="542" alt="image" src="https://github.com/user-attachments/assets/414481e8-a24c-44f0-a01d-bf99a589db8c" />

<img width="1310" height="530" alt="image" src="https://github.com/user-attachments/assets/e5ff9997-3d0a-423d-bec1-900d96aea5cd" />

3. Utilize the Project-based Matrix Authorization Strategy to assign overall read permission to the john user.

<img width="1365" height="507" alt="image" src="https://github.com/user-attachments/assets/7dc52c19-7437-4600-bbf3-dbf08b02d1bb" />


4. Remove all permissions for Anonymous users (if any) ensuring that the admin user retains overall Administer permissions.

<img width="1327" height="583" alt="image" src="https://github.com/user-attachments/assets/a321c7f9-8759-4519-a5da-cc72053382cd" />


5. For the existing job, grant john user only read permissions, disregarding other permissions such as Agent, SCM etc.


Note:

1. You may need to install plugins and restart Jenkins service. After plugins installation,
select Restart Jenkins when installation is complete and no jobs are running on plugin installation/update page.




2. After restarting the Jenkins service, wait for the Jenkins login page to reappear before proceeding. Avoid clicking Finish immediately after restarting the service.


3. Capture screenshots of your configuration for review purposes. Consider using screen recording software like loom.com for documentation and sharing.



## Solution
