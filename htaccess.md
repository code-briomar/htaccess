## .htaccess
---

The `.htaccess` file is a confirguration file that controls how the web server responds to requests.

It only operates within the directory it is in.

> Uses of .htaccess

* Redirecting URLs.
* Enabling password protection.
* Improving SEO.
* Displaying custom error pages.

`.htaccess` stands for **HyperText access**

1. Error Handling

A web server responds to a request by delivering output. If something goes wrong an error is generated. Different errors have different error codes.

*Client Request Errors*
---

400 — Bad Request

401 — Authorization Required

402 — Payment Required (not used yet)

403 — Forbidden

404 — Not Found

405 — Method Not Allowed

406 — Not Acceptable (encoding)

407 — Proxy Authentication Required

408 — Request Timed Out

409 — Conflicting Request

410 — Gone

411 — Content Length Required

412 — Precondition Failed

413 — Request Entity Too Long

414 — Request URI Too Long

415 — Unsupported Media Type.

*Server Errors*
---

500 — Internal Server Error

501 — Not Implemented

502 — Bad Gateway

503 — Service Unavailable

504 — Gateway Timeout

505 — HTTP Version Not Supported.


By default if any of the erros occurs the server will display generic message on the screen which is not usually ideal.

Create a file to be displayed when the error is generated.

The `.htaccess` command to specify this is

```.htaccess
ErrorDocument 404 /htaccess/not_found.html
```

htaccess is the folder containing the error_handler file

2. Password Protection

*.htpasswd*
---
Usernames and Passwords for the .htaccess system are stored in a file name .htpasswd

They are stored in a single line in the form:

```htaccess
username:encryptedpassword
```

for example

```htaccess
johnsmith:F418zSM0k6tGI
```

The password stored in the .htpasswd is the cryptographic hash of the password.

3. Specifying a default file for a directory

```htaccess
DirectoryIndex home.html
```

You can also specify more than one DirectoryIndex

```htaccess
DirectoryIndex index.php index.shtml index.html
```

.htaccess affects its own directory and sub directories. The sub directories might have default pages that are unique. This is the importance of specifying more than one.

4. Disable or Enable Directory browsing

### disable directory browsing
```htaccess
Options All -Indexes
```

### enable directory browsing
```htaccess
Options All +Indexes
```

5. Block Access to a Comprehensive Range of Files


If you want to protect particular files, or even block access to the .htaccess file, try customising the following code:

```htaccess
<Files privatefile.jpg>
 order allow,deny
 deny from all
</Files>

<FilesMatch ".(htaccess|htpasswd|ini|phps|fla|psd|log|sh)$">
 Order Allow,Deny
 Deny from all
</FilesMatch>
```

6. To remove the .php extension from a PHP file for example yoursite.com/wallpaper.php to yoursite.com/wallpaper you have to add the following code inside the .htaccess file:

```htaccess
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^([^\.]+)$ $1.php [NC,L]
```