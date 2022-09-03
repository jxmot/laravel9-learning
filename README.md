# Please note that this is currently a "work in progress"

---
---

# laravel9-learning

This repository will contain information and source code related to Laravel 9.

## Goals



## Anti Goals


# Development Environment

This is my set up, yours does not have to match. But you will need an OS of your choice and an editor and a web browser:

* OS: Windows 10 Pro 64bit
* Browser & Dev tools: Chrome 104+
* Editor: Notepad++ v8.4.4
* Version Control: git 2.37

Here are the versions of the required components I'm using:

* Composer 2.3.10
* PHP 8.1.6
* MySQL 5.7.38 Community
  * MySQL Workbench 8.0

For the **front end** we will be using:

* Bootstrap v4.6.2
* jQuery v3.6.0
* Font Awesome 4.7.0

You won't need to download or install any of the front end components, they're included in the repository.

# Before You Begin

Hopefully you landed here before diving into the multitude of Laravel 9 tutorials. 

Why? Because I've done that for you. I have gone through many Laravel tutorials(*good **and** bad*) and collected useful and *correct* directions and information.

The tutorials and related source code files you will find here have been *tested* and are *working*. And that's because I actually use the code and procedures you will find here.

## Your Existing Knowledge

It would be a benefit for you if you already possess basic understanding of:

* PHP and its syntax
* HTML / CSS syntax
* CLI commands for your OS
* Using MySQL Workbench (*user creation, schema creation, table manipulation, viewing table data*)

# No Docker Required

First, you really don't need to have Docker installed to begin using Laravel. It only depends on how you're already set up or what your development preferences are. And perhaps what you're targeting for deployment.

I don't have anything against Docker. In fact I like it, for certain purposes. But it's definitely **not required** for what we're doing here.

# Easy Bootstrap 4

Or, you can use Bootstrap 5 if you prefer. The steps will be the same for either version. But I've already downloaded it and it's included in the repository along with jQuery and Font Awesome.

## No Node Needed

We won't need NodeJS because we're not doing anything that will require it. 

# Ready?

- [ ] PHP >= 8 is installed
- [ ] Composer >= 2.3 is installed
- [ ] MySQL 5.7 and MySQL Workbench are installed

In MySQL Workbench you will also need to:

- [ ] Create a "schema", name it **`laravel_learn`**
- [ ] Create a "user", name it **`laravel_user`**
  - [ ] Give appropriate permissions to the user for all tables under the **`laravel_learn`** schema.

The reason 

And you will need to:

- [ ] Download this repository as a zip file and unzip it on your PC
- [ ] Enter the repository folder either via the CLI or using a "file explorer"

# This Repository

## Folder Organization



**VERIFY**
You can safely remove:

* All controllers.
* The User model.
* The database factory and migrations.
* The example tests.
* The routes defined in the routes/{api,channels,console,web}.php files (but not the files themselves).
* The JS and SASS in resources/
* The example view in resources/views/
**VERIFY**



# Bootstrap Horizontal Menu




# Simple CRUD




# Development

## Prerequisites

### Minimal

## Set Up For Development

## Laravel 9 Project Installation








# Production

## Prerequisites

## Set Up For Production

## Laravel 9 Project Installation

## Deployment Options

