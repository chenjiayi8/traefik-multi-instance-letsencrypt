# traefik-multi-instance-letsencrypt

This repository contains a sample setup using Docker Compose, Nginx and Traefik to demonstrate how multiple instances of Traefik can be used in conjunction to handle HTTP to HTTPS redirection and domain-specific routing with unique Let's Encrypt certificates.

# Let's Encrypt Configuration

## 1. Create the necessary directories for Let's Encrypt to store its files:

```
mkdir -p ./letsencrypt/abc/
mkdir -p ./letsencrypt/efg/
```

## 2. Create the `acme.json` file in each directory:

```
touch ./letsencrypt/abc/acme.json
touch ./letsencrypt/efg/acme.json
```

## 3. Set the permissions on the `acme.json` file:

```
chmod 600 ./letsencrypt/abc/acme.json
chmod 600 ./letsencrypt/efg/acme.json
```

# Testing this locally

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

This will start your Docker containers in the background. Now, you should be able to access your services locally by navigating to `https://abc.com` and `https://efg.com` in your web browser.

Please note that changing the hosts file requires administrative privileges, and you may need to restart your machine or clear your DNS cache for the changes to take effect.

# Testing in Production

`Replace the placeholder domains with your actual domain names`: Replace "abc" and "efg" with your actual domains.

`Switch Let's Encrypt to Production`: In the Traefik service, change the caServer from the Let's Encrypt staging server to the production server by removing or commenting out the line:

```
- "--certificatesresolvers.abc.acme.caServer=https://acme-staging-v02.api.letsencrypt.org/directory"
- "--certificatesresolvers.efg.acme.caServer=https://acme-staging-v02.api.letsencrypt.org/directory"
```

`Remove Insecure API`: Remove `--api.insecure=true` from the Traefik services, which makes the Traefik dashboard and API available without any security. In a production setting, you would want to secure the Traefik dashboard behind some sort of authentication.
