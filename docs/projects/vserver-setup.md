# V-Server Setup

<!--INSERT YOUR BRIEF DESCRIPTION HERE -->
This project includes a local Ubuntu Server environment used to practice and document basic server administration and DevSecOps concepts.

The server was set up as a virtual machine using VirtualBox and Ubuntu Server. The following steps were completed as part of the server setup.

## Table of Contents

<!--INSERT YOUR TABLE OF CONTENTS HERE -->
- [Quickstart](#quickstart)
- [Description](#description)
- [Further References](#further-references)

import GithubLinkAdmonition from '@site/src/components/GithubLinkAdmonition';

<GithubLinkAdmonition 
    link="https://github.com/DaveHannemann/my-dso-blog/blob/main/docs/projects/vserver-setup.md"
    title="Github Tip" 
    type="tip"
/>

## Quickstart

1. Create a SSH-Key pair on local machine

    ```bash
    ssh-keygen -t ed25519
    ```

2. SSH-Key Authentication
    Add the public key to your server's authorized_keys

    ```bash
    ssh-copy-id -i ~/.ssh/id_ed25519.pub name@ip.addr
    ```

3. Test Login using SSH

    ```bash
    ssh name@ip.addr
    ```

4. Disable Password Login

    ```bash
    sudo nano /etc/ssh/sshd_config
    ```

    Find the line 

    ```bash
    #PasswordAuthentication yes
    ```

    and change it to

    ```bash
    PasswordAuthentication no
    ```

    now restart the SSH service

    ```bash
    sudo systemctl restart ssh.service
    ```

5. Login Check
    Verify that password-based authentication is disabled by attempting
    an SSH login without public-key authentication:

    ```bash
    ssh -o PubkeyAuthentication=no name@ip.addr
    ```

    Result should look like:

    ```bash
    name@ip.addr: Permission denied (publickey).
    ```

6. Install NGINX

    ```bash
    sudo apt update 
    sudo apt install nginx
    ```

    Check for activation
    ```bash
    sudo systemctl status nginx.service
    ```
    and use your ip.addr in your preffered browser see the nginx standard page

7. Create an alternative site for NGINX

    Create a directory for alternatives, if it does not exist yet
    ```bash
    sudo mkdir /var/www/alternatives/
    ```

    then create a new file alternate-index.html in this directory
    ```bash
    sudo nano /var/www/alternatives/alternate-index.html
    ```

    add the following or your own alternative:
    ```bash
    <!doctype html>
    <html>
    <head>
            <meta charset="utf-8">
            <title>Hello, Nginx!</title>
    </head>
    <body>
            <h1>Hello, Nginx!</h1>
            <p>I have just configured the Nginx web server on my local Ubuntu Server!</p>
    </body>
    </html>
    ```
    
    add a configuration for nginx alternatives
    ```bash
    sudo nano /etc/nginx/sites-enabled/alternatives
    ```
    
    The configuration:
    ```bash
    server {
            listen 8081;
            listen [::]:8081;

            root /var/www/alternatives;
            index alternate-index.html;

            location / {
                    try_files $uri $uri/ =404;
            }
    }
    ```

    Restart your nginx service
    ```bash
    sudo service nginx restart
    ```

    and test your alternatives with
    ```bash
    http://ip.addr:8081
    ```

8. Connect your Server with Git
    ```bash
    git config --global user.name "GitUserName" 
    git config --global user.email "your-git-email@example.com"
    ```

    Create another SSH-Key pair on your server for GitHub authentication

    ```bash
    ssh-keygen -t ed25519 -C "your-git-email@example.com"
    ```
    The public key was then added to GitHub under **Settings → SSH and GPG keys**.

    Test it with:
    ```bash
    ssh -T git@github.com
    ```

    if this message will be shown:
    ```bash
    Hi GitUserName! You've successfully authenticated, but GitHub does not provide shell access.
    ```
    you have successfully connected to GitHub via SSH

## Description

This project documents the setup of a local Ubuntu Server environment using VirtualBox.

The purpose of this project is to practice basic server administration and DevSecOps concepts, including SSH key authentication, SSH hardening, NGINX configuration, Git configuration, and SSH-based authentication with GitHub.

The server is running locally in a virtual machine and is used as a learning environment for the practical implementation of the required server setup.

## Further References

- [OpenSSH Documentation](https://www.openssh.com/manual.html)
- [NGINX Documentation](https://nginx.org/en/docs/)
- [GitHub Docs - Connecting to GitHub with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)