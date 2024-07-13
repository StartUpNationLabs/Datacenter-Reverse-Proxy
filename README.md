# Nginx Conf

## Main Conf

- [nginx.conf](nginx.conf)
- [json_log_format.conf](json_log_format.conf)

## Sites Conf

- [adakite.conf](sites-available/adakite.conf)
- [ax-vm.conf](sites-available/ax-vm.conf)
- [basalt.conf](sites-available/basalt.conf)
- [granite.conf](sites-available/granite.conf)
- [obsidian.conf](sites-available/obsidian.conf)
- [ozeliurs.conf](sites-available/ozeliurs.conf)


# Cetificates

Install [ACME.sh](https://github.com/acmesh-official/acme.sh) with the [get.acme.sh](https://github.com/acmesh-official/get.acme.sh) script.

```bash
curl https://get.acme.sh | sh

# -- or --

wget -O -  https://get.acme.sh | sh
```

Make sure to set the environment variables for cloudflare configuration.

```bash
export CF_Token="blahblah"    # Go to Cloudflare Profile for a domain, API Tokens, create a token with Zone:DNS:Edit permission
export CF_Account_ID="blahblah"   # Go to Cloudflare Global for a domain, account ID is at the bottom right
```

## Issue Certificates

Alias to generate a certificate for a domain and its subdomains.

```bash
gen_crt() {
    local domain="$1"
    acme.sh --issue --dns dns_cf -d "$domain" -d "*.$domain" --key-file "/home/debian/.acme.sh/pem/$domain-privkey.pem" --fullchain-file "/home/debian/.acme.sh/pem/$domain-fullchain.pem";
}
```

Generate a certificate for a domain and its subdomains.

```bash
gen_crt ozeliurs.com
```

All current domain to generate a conf:

```bash
gen_crt adakite.ozeliurs.com
gen_crt ax.oze.li
gen_crt basalt.ozeliurs.com
gen_crt granite.ozeliurs.com
gen_crt obsidian.ozeliurs.com
gen_crt ozeliurs.com
```