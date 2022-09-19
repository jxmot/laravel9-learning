
# Hosting a Laravel Application

These instructions will cover installing a Laravel application so that it is accessible via a subdomain on an internet accessible server. 

For example - 

`https://laravelapp.example.com`

Note: the following substitutions are used in this document:

* `[USER]` = the domain's primary user
* `[APPDIR]` = the folder where Laravel will be installed
* `[SUBDOM]` = subdomain name

These instructions will take you to a point where a "basic" Laravel application will be installed **without** any modifications. 

# Getting Started

Required:

* A web accessible server with **cPanel management**
* The server will require:
  * php >=8.0
  * composer >=2.2
  * MySQL >=5.6
  * SSH access for a terminal and file transfer
    * The Bitvise SSH client is recommended

Before you start make sure that:

* Your domain's disk quota is set appropriately. The basic Laravel installation will need about 50mb. Additional space will be used by your application-specific source files and other content.
* Your domain has enough allowed databases, typically one is required by a Laravel application.
* Your domain has subdomains enabled, and at least one is allowed.

## Database Set Up

At the server go to "Databases -> MySQL® Databases":

a) Create a new database, and give it an appropriate name.
    `[USER]_invapp_db` (the `[USER]` portion is automatic, you will be adding the `_invapp_db` part)
b) create user(s) for the new database
    `[USER]_invapp_user` (same as the database names)

**NOTE**: cPanel does NOT indicate any database <-> user association.

## Prepare for Laravel Installation

Prepare for Laravel installation(can be done via terminal or SFTP/FTP, if not it will be noted):

a) navigate to `/home/[USER]/public_html`
b) to keep things organized create a folder named `subdoms`. It will be the location that contain folders that will be the path for a subdomain
c) navigate into `subdoms`
d) create a folder to contain your Laravel installation, name it something appropriate to your application. Such as `blog`, `inventory`, `recipes` and so forth. Abbreviations can be used as long as you remember what they belong to. This will be referred to as `[APPDIR]` from this point forward in this document.


## Install Laravel

Installing Laravel will require the use of the terminal:

a) navigate to `/home/[USER]/public_html/subdoms/[APPDIR]`
b) run this to install Laravel:
    `composer create-project laravel/laravel --prefer-dist .`

c) if successful this folder will now contain a "basic" Laravel installation.

## Subdomain Setup

Set up the subdomain via cPanel:

a) Go to "Domains -> Subdomains" in cPanel
b) enter a name in "Subdomain" field, this will be referred to as `[SUBDOM]` later in this document
c) in the "Document Root" field enter this - `subdoms/[APPDIR]/public`
d) click "Create"

To test the installation use your browser and navigate to:
            `http://[SUBDOM].example.com/`

You should see the default Laravel splash page.


## Enable HTTPS

To enable httpS and force http -> https:

1) navigate to `/home/[USER]/public_html/subdoms/[APPDIR]/public`
2) edit `.htaccess`and just below the `RewriteEngine On` line add the following two lines and save the file:

      `RewriteCond %{HTTPS} !=on`
      `RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]`

3) navigate to `/home/[USER]/public_html/subdoms/[APPDIR]/app/Providers`
4) edit `AppServiceProvider.php`, add the following to the `boot()` function:
       `\URL::forceScheme('https');`

Now if you take your browser and go to `http://[SUBDOM].example.com/` it will automatically switch to httpS.

# Important Notes

**IMPORTANT!!!** When copying your application source onto the server do not overwrite the changes made in the [Enable HTTPS](#enable_https) steps above. 




