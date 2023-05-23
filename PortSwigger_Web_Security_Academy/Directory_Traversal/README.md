# Lab Walkthroughs

##### File path traversal, simple case
[lab 1](lab1/lab1.md)

##### File path traversal, traversal sequences blocked with absolute path bypass
[lab 2](lab2/lab2.md)

##### File path traversal, traversal sequences stripped non-recursively
[lab 3](lab3/lab3.md)

##### File path traversal, traversal sequences stripped with superfluous URL-decode
[lab 4](lab4/lab4.md)

##### File path traversal, validation of start of path
[lab 5](lab5/lab5.md)

##### File path traversal, validation of file extension with null byte bypass
[lab 6](lab6/lab6.md)

# Directory Traversal
Directory traversal is a web application vulnerability that allows an attacker to insert traversal sequences (`../`) into a file path. This allows an attacker to arbitrarily read files on the backend system, read web application source code, access user credentials, and in some cases, upload files and completely take over the server.

An example of directory traversal could look like the following.
`http://someurl.com/photo?filename=../../../../../../etc/passwd`

The application serves photos through a user-controlled parameter that has little to no defenses against traversal attacks. This means instead of loading an image like the above request is supposed to, the `/etc/passwd` file would be displayed to the screen instead.

## Preventing Directory Traversal
The most effective way to prevent traversal attacks is to never supply user-controlled input to file system APIs.

Most applications that do provide user-controlled input to file system APIs can be rewritten to provide the same functionality in a safer manner.

If the application can be rewritten in this manner, two layers of defense should be implemented as follows

- The application should validate input by comparing the provided user input to a whitelist of permitted values. From there the user input should then be stripped to only allows alphanumeric characters.

- Next, the application should append the supplied input to the base directory and use a file system API to canonicalize the path. This should verify if the overall path starts with the expected base directory.

The following example shows how the above defenses could be implemented in Java
```Java
final String BASE = "/var/www/uploads/"

File f = new File(BASE, userInput);
if (f.getCanonicalPath().startsWith(BASE_DIRECTORY)) {
    // process file
}
```