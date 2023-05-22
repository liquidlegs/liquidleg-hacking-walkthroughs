# Lab 1
##### Exploiting XInclude to retrieve files

![1](assets/1.png)

As in the last few exercise, this lab has a vulnerability located in the "check stock" feature, however at first glance there does not appear to be any xml that is submitted in the request.

![2](assets/2.png)

However, when the Xinclude feature is utilized to include `/etc/passwd` on the local system, the user is able to read internal files on the server without the need of inserting or creating an xml entity.

![3](assets/3.png)
