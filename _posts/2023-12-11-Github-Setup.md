---
title: Work With Multiple Github Accounts on The Same Computer
date: 2023-12-12 08:35:01 +/-TTTT
tags: git     # TAG names should always be lowercase
---

Swapping between my personal github account and school account was a challenge at first, but following a clear naming process made my life much easier.

This guide describes a clean configuration of multiple github accounts on a mac device. Commands may differ for other operating systems.

## Steps
1. Create SSH keys for both accounts
2. Adding your SSH Keys to the ssh-agent
3. Create a Config file and make host entries
4. Add your SSH Keys to github
5. Cloning github repositories using different accounts


## 1. Create SSH keys for both accounts
First navigate to your `.ssh` folder to view any existing SSH keys.
```shell
$ cd ~/.ssh
```
{: .nolineno }
Remove unused keys or old keys as necessary.

Then generate a unique SSH key for each github account.
```shell
$ ssh-keygen -t ed25519 -C "your_email@example.com" -f "key_file_name"
```
{: .nolineno }
In my case, I named each `"key_file_name"` after my seperate github usernames.
```shell
$ ssh-keygen -t ed25519 -C "my_personal_email@gmail.com" -f "eboos3"
$ ssh-keygen -t ed25519 -C "my_school_email@gmail.com" -f "eboos7"
```
{: .nolineno }
You should see this create 4 new files in your `.ssh` folder. When you generate a key pair with `ssh-keygen`, it creates two files: one is the private key, and the other is the public key with a .pub extension. 

In my case, I have an eboos3, eboos3.pub, eboos7, and eboos7.pub files. 
## 2. Adding your SSH Keys to the ssh-agent
Start the ssh-agent in the background.
```shell
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```
{: .nolineno }
## 3. Create a Config file and make host entries
If you do not have a `config` file in your `.ssh` folder create one using the touch command.
```shell
$ touch config
```
{: .nolineno }

Otherwise open the file using the `open` command (vim or emacs works too).
```shell
$ open config
```
{: .nolineno }
Now we add these lines to the file, each block corresponding to each account we created earlier.
```
#eboos7 personal account
     Host personal
          HostName github.com
          User git
          IdentityFile ~/.ssh/eboos7

#eboos3 school account
     Host school
          HostName github.com
          User git
          IdentityFile ~/.ssh/eboos3
```
{: .nolineno }
The `config file defines simplified aliases for connecting to specific servers with predefined settings like hostnames, user names, identity files (SSH keys), and custom ports.

## 4. Add your SSH Keys to github
Copy the SSH public key to your clipboard. Replace eboos3 with your public key name.
```shell
$ pbcopy < ~/.ssh/eboos3.pub
```
{: .nolineno }

Navigate to the corresponding github account > your profile photo > settings

In the "Access" section of the sidebar, click  SSH and GPG keys. Click New SSH key or Add SSH key. Name the key and paste the clipboard value into the Key field. Click Add SSH Key. 

Set your environment variables.
```shell
$ git config user.name "your_github_username"
$ git config user.email "your_github_email"
```
{: .nolineno }

Test your connection.
```shell
$ ssh -T git@github.com
> Hi eboos7! You've successfully authenticated, but GitHub does not provide shell access.
```
{: .nolineno }

Repeat this process for each ssh key you create.

If you receive an error at this stage, proceed with troubleshooting. Most likely you have one of the following errors:
1. **SSH Key Not Added to GitHub Account:**
Ensure that your public SSH key (~/.ssh/id_rsa.pub or similar) is added to your GitHub account. You can add the SSH key in the SSH and GPG keys section of your GitHub account settings.

2. **SSH Key Not Loaded into SSH-Agent:**
If you are using an SSH key that has a passphrase, ensure that your key is loaded into the SSH agent. You can add your key to the SSH agent by running:
```shell
$ ssh-add ~/.ssh/your-ssh-key
```
{: .nolineno }
Replace your-ssh-key with the name of your private key file.

Complete this set of instructions for each github account and key. Be careful to add the corresponding keys to the correct accounts.

## 5. Cloning github repositories using different accounts
Now we are done with our setups and it is time to see it in action. We will clone a repository using one of the account we have added.

Make a new project folder where you want to clone your repository and go to that directory from your terminal.

In order to use specific accounts for specific projects, we have clone repositories using a different syntax than the normal `git clone` command.

The normal `git clone` command is as follows.

```shell
$ git clone git@github.com:{owner-repo-user-name}/{the-repo-name}.git
```
{: .nolineno }
Our new syntax that specifies which git account we are working with.

```shell
$ git clone {config-host-alias}:{owner-repo-user-name}/{the-repo-name}.git
```
{: .nolineno }

So, to clone the [chirpy website theme](https://github.com/cotes2020/jekyll-theme-chirpy) for this blog into my personal account I would run the following command.
```shell
$ git clone personal:cotes2020/jekyll-theme-chirpy.git
```
{: .nolineno }
Notice **"personal"** is the Host name for my personal account inside of the Config folder.

## Conclusion
From now on, to ensure that our commits and pushes from each repository on the system uses the correct GitHub user — we will have to configure user.email and user.name in every repository freshly cloned or existing before.

To do this use the following commands.
```shell
$ git config user.email "my_personal_email"
$ git config use.name "eboos7"

$ git config user.email "my_school_email"
$ git config use.name "eboos3"
```
{: .nolineno }
Pick the correct pair for your repository accordingly.

To create a repository from scratch simply use the following commands

```shell
$ git init

$ git remote add origin {alias-from-config}:{github-username}/{new-repository}.git
```
{: .nolineno }

### Other Resources
- [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)
- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [Georgia Tech Github Setup](https://webmasters.gatech.edu/handbook/connecting-github-enterprise-command-line)
- [Similar guide](https://gist.github.com/rahularity/86da20fe3858e6b311de068201d279e3)