# Lab 2
##### Information disclosure on debug page

![1](assets/1.png)

After loading the page intercepting the http traffic with burp proxy, an interesting path can be seen in the web application sitemap found in the burp interface at `Target` -> `Sitemap` named `cgi-bin/phpinfo.php`

![2](assets/2.png)

Browsing to this page reveals a wealth of information about what plugins are enabled, application features, environment variables, internal system directory, etc.

![3](assets/3.png)

Scrolling down the phpinfo page, the secret key required to complete the lab can be found in the servers environment variables.

![4](assets/4.png)

The phpinfo page should always be removed the server before deploying a php application in a production enviornment.