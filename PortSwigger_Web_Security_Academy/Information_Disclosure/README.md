# Information Disclosure - Lab Walkthroughs

##### Information disclosure in error messages
[lab 1](lab1/lab1.md)

##### Information disclosure on debug page
[lab 2](lab2/lab2.md)

##### Source code disclosure via backup files
[lab 3](lab3/lab3.md)

##### Authentication bypass via information disclosure
[lab 4](lab4/lab4.md)

##### Information disclosure in version control history
[lab 5](lab5/lab5.md)

## What is information disclosure?
Information disclosure is when sensitive data is internally disclosed to users. Applications can reveal all sorts of information which can be very beneficial to anyone who might break in.

Data that can be disclosed includes:
- Internal directory structures
- Internal usernames and credentials
- Bank account information
- Customer details
- Technical details about the application and the underlying infrastructure

The severity of leaking customer details and bank account information can be quite dangerous to the company, but deeper technical information can be just as dangerous and useful in the hands of an attacker.

Exposing technical information such as specific version numbers for any of the software being utilized on the backend system can be potentially used by attackers to search for any known vulnerabilities that they may be able to exploit or chain with a vulnerability in the application to perform a high severity attack.

It is rare, but sometimes you will find that sensitive data is disclosed to users by using the application in the way it was designed to be used. Most commonly, you would have to interact with the application in a way that the developers did not intend. This could be achieved by attempting to access pages or apis in an order or fashion that requires a specific process, that the application does not account for.

This could be done by trying to add a new user to the application without first logging in. Providing input that the application does not expect or attempting to make requests to a page with the `TRACE` method instead of the `POST` method may leak sensitive technical information about the backend.

## Examples of information disclosure
- backend directory structure names
- Internal usernames and credentials
- Custom security header fields
- Explicitly mentioning database and column names in error messages
- Specific version numbers of frameworks and backend software
- Enabled and disabled features
- Hardcoded credentials, API keys, and Ip Addresses in source code
- Source backup files
- Files like `robots.txt` and `sitemap.xml` that may have public and private directory names and files
- Debug files like `phpinfo.php`
- Debug logs
- Credit card details
- Hinting at the absence of users or resources
- Developers have forgotten to remove the `.git` directory in production. As a result source code can be obtained through viewing the commit history.

## How information disclosure arises
Information disclosure vulnerabilities arise in a number of ways and are categorized as follows.

- ***Failure to remove developer content from public content***: Sometimes developer comments leaking sensitive information may be found in HTML markup.
- ***Server misconfigurations***: failing to disable debug logs and diagnostic features. Default server configurations can also leave the server vulnerable. An example of this is not deleting, disabling, or changing the password of the default administrator account.
- ***Flawed design and behaviour***: Some applications may return distinct error status codes when in certain error states. This may be useful to an attacker to perform user or credentials enumeration.

## The impact of information disclosure
The impact of information disclosure depends on the information that has been leaked. For example: leaked credit card and bank account information is likely going to have critically severe consequences for being leaked.

Leaking internal/backend usernames may have little to no consequences attached to it, however, it will depend on what the attacker can or can't do with the information.

## Preventing information disclosure
Below are the best practices used by cybersecurity professionals to prevent information disclosure:

- Audit any code for potential information disclosure as part of your QA or build processes
- Automate the removal of developer comments and similar associated tasks
- Use generic error messages as much as possible that do not disclose internal application behaviour
- Double-check that all diagnostic and debugging features have been disabled.
- Disable/remove any features and settings that you do not need