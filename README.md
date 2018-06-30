# Linux Server Configuration Project - FSND

---

A linux virtual machine is configured to support the Item Catalog application from my other repository. You can access the website by either through the Ip address or through the hostname url provided below.

### (Important Note: Login is only accessible through the url pathing.)
---
* Ip address: 52.36.67.3
* Port: 2200
* 8URL: ec2-52-36-67-3.us-west-2.compute.amazonaws.com

#### Summary of software installed (aside from package updates):
---
* mod_wsgi
* Apache2 
* Virtualenv (venv)
* finger
* python

Summary of Linux Configurations made:
---
* Create an the instance through Amazon Lightsail
* Create and then attach a static ip to the instance
* Add additional ports 123 and 2200 to the firewall
* Save a private key (.pem) and move it to the ```.ssh``` folder in the local directory
    * Use that same key and create a Public key (.rsa) and (.rsa.pub)
* Log into the instance through Lightsail
* create a new user named: grader
    * Give grader the same permission access as root
    * Create an ```.ssh``` folder under grader's directory
        * Create an ```authorized_keys``` file within that folder
        * Copy the public key content made from before and paste it within ```authorized_keys```
* Install all current packages 
* Rewrite part of ```/etc/ssh/ssdh_config```:
    *  Change the port so it's now 2200 and not 22
    * Change ```PermitRootLogin``` to no
    * Change ```PasswordAuthentication``` to no
        * Restart ssh changes were made
        * Double check that the changes were made through attempting to access through the local directory
* Configure the Uncomplicated Firewall to only allow these ports:
    * 2200/tcp
    * 80/tcp
    * 123/udp
        * Then enable the firewall
        * Check that it works by attempting to acess through other ports such as port 22

Summary of Application Configurations made
---
* Install git
* Install Apache
    * change owner and permisson of ```/var/www/``` to grader
* Install mod_wsgi
* Install Psql
    *  Change into the psql super user: ```$sudo su - postgres```
    *  Enter ```psql```
    *  Create a new user along with it's passord
        *  alter the user's role to create databases
    *  Create the ```Catalog``` database
    *  Alter the shema of the database
* Clone the Item Catalog app from the github repository into ```/var/www/```
    *  Change the name of the directory ```item-catalog``` to ```catalog```
    *  Create the ```catalog.wgsi``` file and insert the appropriate code
    *  Within ```__init__.py```, change the pathing anytime ```client_secrets.json``` is being opened
    *  Change the pathing of the database in all ```.py``` files within the directory
    *  ```sudo pip install`` all packages and modules used in the program (including flask)
* Create the ```catalog.conf``` file within ```/etc/apache2/sites-available/``` and type the appropriate code so it.
* Finally, restart the apache server

This is the quick rundown of what I have done to setup the instance as well as the application. Now, the application is accessible through the ip address and the hostname.

---

References and very special thenk yous:

* https://ubuntuforums.org/showthread.php?t=1739013
* https://askubuntu.com/questions/27559/how-do-i-disable-remote-ssh-login-as-root-from-a-server
* https://www.dabapps.com/blog/introduction-to-pip-and-virtualenv-python/
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps