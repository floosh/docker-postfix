docker-postfix
==============

Forked from https://github.com/catatnight/docker-postfix

It's the same idea (TLS + OpenKDIM) but SASL is disabled.
This postfix instance can be only used from another container with IP like 172.17.x.x (docker defaults)

## Requirement
+ Docker 1.0

## Installation
1. Build image

	```bash
	$ sudo docker pull floosh/postfix
	```

## Usage
1. Create postfix container

	```bash
	$ sudo docker run -p 25:25 --name postfix -d floosh/postfix
	```
	
2. Enable OpenDKIM: save your domain key ```.private``` in ```/path/to/domainkeys```

	```bash
	$ sudo docker run -p 25:25 \
			-v /path/to/domainkeys:/etc/opendkim/domainkeys \
			--name postfix -d floosh/postfix
	```
3. Enable TLS(587): save your SSL certificates ```.key``` and ```.crt``` to  ```/path/to/certs```

	```bash
	$ sudo docker run -p 587:587 \
			-v /path/to/certs:/etc/postfix/certs \
			--name postfix -d floosh/postfix
	```

## Note
+ You can assign the port of MTA on the host machine to one other than 25 ([postfix how-to](http://www.postfix.org/MULTI_INSTANCE_README.html))
+ Read the reference below to find out how to generate domain keys and add public key to the domain's DNS records

## Reference
+ [How To Install and Configure DKIM with Postfix on Debian Wheezy](https://www.digitalocean.com/community/articles/how-to-install-and-configure-dkim-with-postfix-on-debian-wheezy)
+ TBD
