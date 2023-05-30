# traefik-multi-instance-letsencrypt

This repository contains a sample setup using Docker Compose, Nginx and Traefik to demonstrate how multiple instances of Traefik can be used in conjunction to handle HTTP to HTTPS redirection and domain-specific routing with unique Let's Encrypt certificates.

# Testing this on a local machine

Before you can run your services locally, you will need to map the domains `abc.com` and `efg.com` to your local machine. This can be done by editing your hosts file.

`On Unix-based systems`: You can find this file at `/etc/hosts`

`On Windows`: You can find this file at `C:\Windows\System32\Drivers\etc\hosts`

Add the following lines to your hosts file:

```
127.0.0.1   abc.com
127.0.0.1   efg.com
```

Save and close the file. The domains `abc.com` and `efg.com` will now resolve to your local machine.

Next, start your Docker services. Navigate to the directory where your `docker-compose.yml` file is located and run the following command:

```
docker-compose up -d
```

This will start your Docker containers in the background. Now, you should be able to access your services locally by navigating to `http://abc.com` and `http://efg.com` in your web browser.

Please note that changing the hosts file requires administrative privileges, and you may need to restart your machine or clear your DNS cache for the changes to take effect.
