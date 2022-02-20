- sources 
	- https://docs.requarks.io/install/docker
# Wiki.js notes
What have I done and how? Steps on the wiki.js deployment. 

## Server 
linode server - cheap and cheerful $5 a month. 

## Install steps
1. apt-get update
2. [rn_1595405568_docker_install_script](../../docker/rn_1595405568_docker_install_script.md)
3. 3 images 
	1. dpage/pgadmin4 
	2. requarks/wiki
	3. postgres
4. docker-compose-pg.yml
5. docker-compoe-pgadmin.yml
6. check / create db `wiki`
7. get an ip of a container? 

```bash
root@localhost:~# docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' wiki-pg
172.19.0.2
```

8. godaddy a records
	1. https://dcc.godaddy.com/manage/dns?domainName=academy-42.com
	2. edit a record to public ip of the linode instance
9. docker-compose-wiki.yml
	1. includes lets encrypt
10. access wiki and set admin account detail
	1. user / passwd
11. set https -  Automatic HTTP to HTTPS Redirect.
	1.  Navigate to the **Administration Area** by clicking on your avatar at the top-right corner of the page.
	2.  From the left navigation menu, click on **SSL**.
	3.  Next to the `Redirect HTTP requests to HTTPS` section, click on **TURN ON** to enable HTTP to HTTPS redirection.
	4.  Any requests made to the HTTP port will now automatically redirect to HTTPS!

Setup and ready to go - now sync with github deepthought. 

## Github sync
From the Docker container with wiki js

`ssh-keygen -t rsa -b 4096`

copy the pub.

Add the key to GitHub

    on deepthought repo
    Click on the Settings tab.
    Click on the Deploy Keys in the left navigation menu.
    Click the Add deploy key button.
    Enter a name of your choice for this key (e.g. wiki) and paste the contents of the public key generated earlier. (file ending in .pub)
    Make sure the Allow write access is checked.
    Click the Add key button.


Configure Wiki.js

    In the Administration Area, click on Storage in the left navigation menu.
    Make sure the Git storage target is checked.
    Click on the Git tab.
    Enter the following settings:
        Authentication Type: ssh
        Repository URI: On your GitHub repository page, in the Code tab, click on the Clone or download green button and copy the URI shown below Clone with SSH.
        Branch: main
        SSH Private Key Path: The path to your private key generated earlier.
            this would be /home/node/.ssh/id_rsa
        Username: Empty
        Password: Empty
        Default Author Email: Should match your GitHub account email.
        Default Author Name: Should match your GitHub account name.
        Local Repository Path: Choose where the repo will be cloned locally or leave the default ./data/repo value.
        Verify SSL Certificate: On
    Set the Sync Direction to PULL
    Set the Sync Schedule to 5 minutes.
    Click the Apply Changes button at the top of the page.
    Wait for the Status panel to update. A new entry for Git should appear in green. If the bar is red, it means you have an error in your configuration. Go back to the Git tab, fix the error and try again.

