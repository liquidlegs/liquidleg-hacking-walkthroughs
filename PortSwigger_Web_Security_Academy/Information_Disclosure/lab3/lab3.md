# Lab 3
##### Source code disclosure via backup files

![1](assets/1.png)

Similar to the last exercise, this web application features some backup source code files which can be used to retrieve the database password.

This backup directory can be seen in the burp sitemap below.
![2](assets/2.png)

The `/backup` path is also disclosed in the robots.txt file found at the root of the application.
![3](assets/3.png)

Navigating to the `/backup` directory reveals the following file.
![4](assets/4.png)

The database password can be seen hardcoded into the database connection string.
![5](assets/5.png)
