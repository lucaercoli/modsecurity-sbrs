# How to configure ModSecurity and the SBRS v1 on Debian GNU/Linux with Apache2 web server

###### Prerequisite: a freshly installed ModSecurity



## Installation Steps 

Follow these general installation and configuration steps

* Step 1:  Clone the SBRS GitHub repository using “git” command line tool

```
git clone https://github.com/lucaercoli/modsecurity-sbrs.git
```

* Step 2:  Create a subdirectory named “sbrs-rules” into the ModSecurity’s directory:

```
mkdir /etc/modsecurity/sbrs-rules
```

* Step 3:  From the previously downloaded GitHub package, copy the file modsecurity.conf into /etc/modsecurity/ and modsecurity_sbrs.load into the folder you just created:

```
cp modsecurity-sbrs/modsecurity.conf /etc/modsecurity/
cp modsecurity-sbrs/modsecurity-sbrs.load /etc/modsecurity/sbrs-rules/
```

* Step 4: Enable the Score-Based Rule Set (SBRS) by editing the ModSecurity configuration settings in Apache and then “/etc/apache2/mods-enabled/security2.conf”, which can take this form:

```
<IfModule security2_module>
SecDataDir /var/cache/modsecurity
Include /etc/modsecurity/modsecurity.conf
Include /etc/modsecurity/sbrs-rules/modsecurity-sbrs.load
</IfModule>
```

* Step 5: Restart the Web server for the changes to take effect:

```
service apache2 restart
```





## Post Configuration: Making sure it works

Once everything is configured properly, test mod_security by sending some malicious requests to Apache web server and see if the requests are being blocked or not.
The following attempt must be blocked and receive the HTTP error code 406 (Not Acceptable):

```
https://YOUR-SERVER/?expect://id
```
