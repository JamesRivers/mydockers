# Nextcloud 
Why? I wanted to see what options are open to me regards a replacement for Dropbox, as I only had a free 2Gb Dropbox account that I have now expired. 

What is `Nextcloud`? - [https://nextcloud.com/about] 

What is my solution that I have put in place? 
- Proxmox node 92, in lab is hosing an LXC CT - a Debian turnkey core. This is hosting a nested Docker engine. LXC CT resources - Memory=4.00Gb, Cores=2, Disk 25Gb. 
- LXC CT holds 2 network interfaces, 1 for lab networks and the other for home router access. Downstream of the LXC CT is a `pfsense` server. 
- New Dir created `nextcloud` 
- Docker Compose file created - see compose file.
- Nextcloud storage is actually mounted from an `S3` bucket in my AWS setup. 
- Nextcloud is accessing via a access and secret key. 
- Nextcloud users have to use a 2fa. 
- Nextcloud `/config/www/nextcloud/config/config.php` edited for trusted domains. 
- Nextcloud port 443 is mapped to a high random tcp port. 
- Home router service created and firewall poked hole
- DNS for `academy-42.com` - sub domain created - `store.academy-42.com` Pointed to home public IP... I know this to change in the months to come. 
- AWS S3 bucket created in my region. 
- AWS IAM for Nextcloud access created. 

