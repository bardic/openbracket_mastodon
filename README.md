# openbracket_mastodon

## Requirements / Recommendations
- [Docker](https://en.wikipedia.org/wiki/Docker_(software)) via [Rancher Desktop](https://rancherdesktop.io)

## Glitch Image

The image used Mastodon is based on [Glitch](https://glitch-soc.github.io/docs/) and [LinxusServer.io](https://github.com/linuxserver/docker-mastodon) and can be found [here](https://hub.docker.com/repository/docker/judohippo/mastodon-glitch) 

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

**swag.env.sample**

- Repalce "EMAIL" with your email address.

- Replace "TZ" with your timezoe

- Replace "URL" with your URL  

---

Once all files environment files and the mastondon.default.conf have been modified, simply run `docker-compose up`

This will generate a letsencrypt folder. Do not delete this. This is your SSL certs and will be managed by and refreshed by `swag`

