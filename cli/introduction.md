---
title: Introducing Siteglide CLI
slug: -A-M-
createdAt: 2021-01-22T14:08:27.000Z
updatedAt: 2023-03-03T08:09:21.000Z
---

Siteglide CLI is a tool that enables you to work on your project from your local editor and has similar behaviours to that of using FTP, in that you can sync up and pull down changes from your website. You will be required to use some terminal commands to use this feature.

## Dependencies&#x20;

The CLI is distributed via Node Package Manager (NPM) and so you will need NodeJS installed on your machine. The easiest way to get this is to visit <https://nodejs.org/> and download the LTS version as this has better support.

Siteglide CLI requires a minimum of NodeJS version 10

## Installing & Updating

You can use the following to install Siteglide CLI.

`npm i -g @siteglide/siteglide-cli `

When an update is released for the CLI, you can use the same command as above to install the updated version.  Please note that the flags for commands below are not available on all versions of the CLI, updating to the latest version will allow you to use all of them.

### Installing on Windows&#x20;

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Windows machine. Feel free to skip ahead to the parts you find the most useful.

<https://www.youtube.com/watch?v=mXnHqrHx0L4>

### Installing on Mac

The following video will give you a complete walkthrough guide for setting up Siteglide CLI on a Mac. Feel free to skip ahead to the parts you find the most useful.

The steps I follow in the video can be found [here](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally#manually-change-npms-default-directory).  If you are using zsh as your shell then the commands here will have to be run against the `~/.zshrc` file, not `~/.profile`. ZSH is the default for Macs since macOS Catalina, to find out which shell you are using you can run `echo ${SHELL}` in terminal. If the `~/.profile` or `~/.zshrc` files do not already exist then you may need to create them first before running the export PATH command

<https://www.youtube.com/watch?v=bKS3368YtvA>

## Commands

These commands should be run from within the project folder.  Commands follow the format of `siteglide-cli <command> <env> <flags>` , so for example if you would like to view the logs of your production environment in "quiet mode", you would run:

`siteglide-cli logs production -q` &#x20;

Please note that some commands may fail if you run them in your users home directory.  We recommend a folder structure such as `siteglide/` and then give each project/site it's own folder.

{% hint style="info" %}
Command flags such as `<command>` `<env>` and `<flags>`  should be replaced with the relevant data. For example, `<env>`  should be replaced with the chosen name for the environment such as `production`.
{% endhint %}

***

### Add

The first time you use the CLI with a project on your device, you will need to create an environment. This is essentially a config file that authorises your connection.

`siteglide-cli add <env> --email me@mydomain.com --url https://my_great_site.com`

You must use the email of your Siteglide partner account to replace me\@mydomain.com and the development domain of the website you are connecting with to replace `https://my_great_site.com`

After your site goes live, you will only be able to add the development domain to an environment, not your main user-facing domain.

{% hint style="warning" %}
Replace with a chosen name for the environment, for example `production`. On larger projects you may have more than one environment to allow you to interact with both staging and production websites.
{% endhint %}

***

### Sync

`siteglide-cli sync <env> `

This command will setup a watcher that will automatically sync file saves and deletions when that action happens on your machine.  To stop the sync running, enter use the shortcut control + c in your terminal.

Flags:

`-l`: Turns on the live reload server. This enables automatic browser reloading of a page when a file is saved in your IDE.

***

### Logs

`siteglide-cli logs <env> `

This command will output the last 20 logs and then a live list of logs from your site. Logs are written by using the log liquid code, for example: `{% log 'Hello World!' -%}` . To stop the logs running, enter use the shortcut `control + c` in your terminal

Flags:
`-f` : Filter log types
`-q` : Quiet mode&#x20;

***

### Version

`siteglide-cli -v`

Check the current version of Siteglide CLI you are running. See the [Siteglide CLI changelog](https://developers.siteglide.com/cli-changelog) to find the latest version number. If you need to update, see the "Installing & Updating" command section above.

***

### Help

`siteglide-cli help`

Generates a list of valid Siteglide CLI commands available to you.

***

### GraphQL

Deprecated - Please see the GUI command below

***

### GUI

`siteglide-cli gui <env>`

This command will open up the GraphiQL and Liquid Evaluator editors locally. This will let you run Graph queries and mutations to test them out before creating them within your site. Also good for quickly getting data out of the database to check.&#x20;

The Liquid evaluator tool lets you quickly test Liquid from the CLI, without having to create and save a page in Siteglide Admin.

To stop the GUI command running, enter use the shortcut `control + c` in your terminal

Flags:
`-o`: Automatically open GraphiQL in default browser

***

### Pull

`siteglide-cli pull <env>` 

This will pull down all files from the site in to a folder named marketplace\_builder within your current directory. During this process it will also overwrite any local versions of files if they already exist. If you have made any changes locally that you have not synced they WILL be overwritten. 

Flags:

`-i`: Ignore assets such as CSS and JS as part of the pull.

`-m`: Provide the name of a module to download.  Note that this will only download that module and not the site as well.  This will only download the `public` folder within the module, if the module only contains a `private` folder then nothing will be downloaded.&#x20;

Note: Assets such as images and videos are not downloaded as part of CLI Pull

***

### Init

`siteglide-cli init `

This will create a blank folder structure within the folder you run the command, which includes all folders that are automatically created for you when making a new website on Siteglide. If these folders already exist, you will receive an error and so it will not overwrite existing files.

***

### Deploy

`siteglide-cli deploy <env> `

If you have made a lot of changes in your codebase, then you can use deploy to re-send all files to your site at once.  Deploy is a single command that will create a .zip  file of your site and then upload that to your website.

Flags:

`-w` : With assets, also deploys your sites `assets` folder, supports total assets of up to 5GB.

***

### Export

`siteglide-cli export <env> `

Export is very similar to Pull, but it will also grab all data.  This command will first grab all data from the site and export it into a data.json  file, then it will run a pull to grab your code base.

Flags:
`-w` : With assets, also download asset files from your instance such as images and PDFs.

`--csv`: Export the data files as CSV instead of JSON. Please note that these CSV's are currently not compatible with the ones that are exported/imported from Siteglide Admin

`-a`: Only export assets and not the sites codebase.  This by default will only export code related assets (CSS/JS etc) within the /assets folder.  It can be mixed with -w above to export all assets

***

### Migrate

`siteglide-cli migrate <env> --url <existing url>`

Download and migrate an existing site to Siteglide using our site import tool. This tool will scrape the existing site, download all of the publicly accessible pages and assets, compress CSS/JS/images.  The migrate command will also convert any existing forms (using the `<form>` tag) to a "form to email" in Siteglide.  When filled in, this will email the user who triggered the CLI migration with an autoresponder.  These forms can then optionally be updated at a later date within Siteglide Admin.

Note: If you are using a Mac, running migrate in your “home” folder may fail.  Please move into a different folder in terminal and then try again.

Flags:

`--url`: Existing sites URL, usually the homepage.  This flag is mandatory

`-n`: No Optimization, skips the CSS/JS and Image optimization&#x20;

`-m`: A number to set the level of recursion that the scraper will search through the site.  For example setting `-m 1` will only follow 1 link deep from the entry page

`-i`: A string to send to the scraper that if found in the URL it will ignore downloading that page.  For example if your blog posts are links such as `site.com/post/post-name` and you wanted to ignore them, you could use the flag `-i /post/` This flag can be used multiple time such as `-i /blog -i /posts/`&#x20;

***

### List

`siteglide-cli list`&#x20;

Output a list of environments you have previously added and their relative URLs for the current folder.



***

### Modules

`siteglide-cli modules <env>`&#x20;

Provides a list of modules installed onto the instance.  These names can then be used in the `pull` command to download the contents of that module.

***

## Debug Mode

Somtimes Siteglide support may ask you to run the CLI in "debug mode".  This provides more output into your terminal so that we can use it to aid in supporting you. To do this, you need to prefix the command you are running with some extra information.  This prefix differs slightly on macOS, Linux and Windows, for example if you were to want to sync to a site with debug mode on:

{% tabs %}
{% tab title="cli" %}
```linux
DEBUG=true siteglide-cli sync production
```
{% endtab %}
{% tab title="macos" %}
```macos
DEBUG=true siteglide-cli sync production
```
{% endtab %}
{% tab title="windows command prompt" %}
```windows
set DEBUG=true && siteglide-cli sync production
```
{% endtab %}
{% tab title = "windows powershell" %}
```
$env:DEBUG='true'; siteglide-cli sync production
```
{% endtab %}
{% endtabs %}

Note, for macOS and Linux, debugging will be turned on for that one command that you prefix.  For Windows, debugging will be turned on for as long as Command Prompt or Powershell is open.  Closing Command Prompt or Powershell and re-opening it will turn debug mode off.

## Changelog

To see the latest changes to the CLI, we have our changelog [here](https://developers.siteglide.com/cli-changelog)