# AWS Profile Switcher
[![Actions Status](https://github.com/99stealth/aws-profile-switcher/workflows/Check%20and%20Test/badge.svg)](https://github.com/99stealth/aws-profile-switcher/actions)
![Vulnerability Check](https://img.shields.io/snyk/vulnerabilities/github/99stealth/aws-profile-switcher)
[![PyPI version](https://badge.fury.io/py/aws-profile-switcher.svg)](https://badge.fury.io/py/aws-profile-switcher)
![GitHub License](https://img.shields.io/github/license/99stealth/aws-profile-switcher)
![Commit Activity](https://img.shields.io/github/commit-activity/w/99stealth/aws-profile-switcher)

The tool which allows you to jump between your profiles in your `~/.aws/credentials`

## Problematics
Well, if you are operating only one AWS account then you will not find this util useful. Problem appears when there are more than 3 accounts under your control. Sure, you can use `--profile` flag with any your aws cli command. But what if you need to run number of commands for several accounts, then make sure you don't forget to add `--profile` to your command or specified the right profile name. 
Another example is about Hashicorp Terraform. Let's imagine that you have one module which you need to apply for several accounts. Unfortunately, terraform doesn't allow you to specify `--profile` and that's logically since Terraform is not about AWS. So, you will need to hardcode your AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY or go to `~/.aws/credentials` and change the `[default]` profile.

## How to install
That's easy just run
```
sudo pip install aws-profile-switcher
```
Or `clone` this repository and run
```
make install
```

## How does it work
### Simple switch
![Simple switch](.media/simple-switch.gif)

What have you seen:
- User called `aws-profile-switcher`
- `aws-profile-switcher` identified that current default is among of all profiles so it allowd to proceed without any aditional operations
- `aws-profile-switcher` asked user to choose new default profile
- `aws-profile-switcher` switched the default

### In case you have a default but no backup for it
![Backup for default](.media/backup-for-default.gif)

What have you seen:
- User called `aws-profile-switcher`
- `aws-profile-switcher` understood that there is no backup for profile that is currently set to default and suggested to make a backup
- User agreed to make a backup and gave it the name
- `aws-profile-switcher` asked user to choose new default profile
- Voila, default is changed and the old default is backed up

### In case there is no default at all
![No default at all](.media/no-default.gif)

What have you seen:
- User called `aws-profile-switcher`
- `aws-profile-switcher` asked user to choose new default profile
- There was no defalut profile at all, so `aws-profile-switcher` has created it

### In case user doesn't want backing up the default
![No backup for the default](.media/no-default.gif)

What have you seen:
- User called `aws-profile-switcher`
- `aws-profile-switcher` understood that there is no backup for profile that is currently set to default and suggested to make a backup
- User disagreed to make a backup
- `aws-profile-switcher` asked to agreed that he/she doesn't want to make a backup
- Default is changed and the old default was not backed up