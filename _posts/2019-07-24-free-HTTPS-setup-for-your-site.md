---
layout: post
title:  Free HTTPS setup for your site
excerpt: Let’s Encrypt is a free, automated, and open Certificate Authority.
author: sondh5
categories: [ Server ]
image: https://letsencrypt.org/images/letsencrypt-logo-horizontal.svg
image_hidden: true
featured: false
status: public
---

5 minutes guide to encrypt your site  
In this article, my current server using nginx and Ubuntu 16.04 hosted by Amazon EC2

#### Setup your server
Certbot supports many webservers and systems, go to https://certbot.eff.org and get your suitable guide.

1. ssh to server
2. Install certbot
  ```
    sudo add-apt-repository ppa:certbot/certbot
    sudo apt-get update
    sudo apt-get install certbot python-certbot-nginx
  ```

3. Edit your Nginx configuration automatically
  ```
    sudo certbot --nginx
  ```
  
#### Setup your instance
1. Go to you EC2 / SecurityGroups
2. Add inbound rule HTTPS - Port 443

#### Confirm Certbot worked and enjoy HTTPS
Test your site at: https://www.ssllabs.com/ssltest/

***

*References*
- [Let’s Encrypt](https://letsencrypt.org/)
- [certbot](https://certbot.eff.org/l)
- [SSL Labs](https://www.ssllabs.com/ssltest/)