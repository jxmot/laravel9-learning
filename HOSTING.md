
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

1) Create a new database, and give it an appropriate name.
    `[USER]_invapp_db` (the `[USER]` portion is automatic, you will be adding the `_invapp_db` part)

2) create a new user for the new database
    `[USER]_invapp_user` (same as the database names)

Make note of the password you created for the user. It will be needed for setting up your Laravel application.

**NOTE**: cPanel does NOT indicate any database <-> user association.

## Prepare for Laravel Installation

Prepare for Laravel installation(can be done via terminal or SFTP/FTP, if not it will be noted):

1) navigate to `/home/[USER]/public_html`

2) to keep things organized create a folder named `subdoms`. It will be the location that contain folders that will be the path for a subdomain

3) navigate into the `subdoms` folder

4) create a folder to contain your Laravel installation, name it something appropriate to your application. Such as `blog`, `inventory`, `recipes` and so forth. Abbreviations can be used as long as you remember what they belong to. This will be referred to as `[APPDIR]` from this point forward in this document.

## Install Laravel

Installing Laravel will require the use of the terminal:

1) navigate to `/home/[USER]/public_html/subdoms/[APPDIR]`

2) run this to install Laravel:

    `composer create-project laravel/laravel --prefer-dist .`

3) if successful this folder will now contain a "basic" Laravel installation.

## Subdomain Setup

Set up the subdomain via cPanel:

1) Go to "Domains -> Subdomains" in cPanel

2) enter a name in "Subdomain" field, this will be referred to as `[SUBDOM]` later in this document

3) in the "Document Root" field enter this - `subdoms/[APPDIR]/public`

4) click "Create"

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

* When copying your application source onto the server do not overwrite the changes made in the [Enable HTTPS](#enable_https) steps above.
* The `.env` file with your application's changes in it will need to be modified. The minimum changes are:

```
DB_DATABASE=[USER]_invapp_db
DB_USERNAME=[USER]_invapp_user
DB_PASSWORD=[password goes here]
```

* The `php artisan...` commands should be run while in the terminal and located in the `/home/[USER]/public_html/subdoms/[APPDIR]` folder.