# Openbracket Mastodon Glitch

A Docker based self-hosted mastodon solution

## Requirements / Recommendations
- [Docker](https://en.wikipedia.org/wiki/Docker_(software))


## Stack

- lscr.io/linuxserver/mastodon:latest
- redis:latest
- postgres:latest
- namshi/smtp:latest
- jc21/nginx-proxy-manager:latest


## Customizations 


### **Confs**
- mastodon.default.conf

Replace "openbracket.ca" on lines 34/35 with your URL 

### **Envs**

Remove .sample from the file names

**mail.env.sample**

- Replace "GMAIL_PASSWORD" with an app password that you can create here: [Google Security](https://myaccount.google.com/security) 

- Replace "GMAIL_USER" with your gmail account 

**mastodon.env.sample**

- Replace SECRET_KEY_BASE with value from `docker run --rm -it -w /app/www --entrypoint rake lscr.io/linuxserver/mastodon secret`

- Replace "OTP_SECRET" with value from `docker run --rm -it -w /app/www --entrypoint rake lscr.io/linuxserver/mastodon secret`


- Replace "VAPID_PRIVATE_KEY" and "VAPID_PUBLIC_KEY" with values from `docker run --rm -it -w /app/www --entrypoint rake lscr.io/linuxserver/mastodon mastodon:webpush:generate_vapid_key` 

- Replace "LOCAL_DOMAIN" with your URL 

- Replace "TZ" with your timezoe

- Replace "SINGLE_USER_MODE" with true if you want to close the registrations and have the index point to the first users page

---

To offer flexibility, this solution used Nignx Proxy Manager to manage our redirects and SSL. Once ready, run `docker-compose up npm`. This will spin up just the NPM server which you can reach `host:81`. The default user and pass is `admin@exmaple.com` and `changeme`. You'll be immeadiately prompted to create a new account. 

Account that is complete we will add a new Proxy host. Here are the details you will need: 

- Domain : your URL
- Scheme : `https`
- Forward Hostname/IP: `mastodon-glitch`
- Port: `443`

Under SSL select request and enable HTTP/2 Support .

And Save! After a moment you should see in your letsencyrpt folder a live folder with your URL as the name. You can now stop NPM. 

Now run `docker-compose up`. This will take a few moments to start up. I suggest getting a coffee. 

Once the server has started you should be able to how hit your URL and have SSL enabled.

