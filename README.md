<p align="center">
    <h1 align="center">SecureNginx — Educational NGINX Templates</h1>
    <br>
    <a href="LICENSE">
        <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT">
    </a>
    <a href="https://github.com/izeleam/securenginx/issues">
        <img src="https://img.shields.io/github/issues/izeleam/securenginx" alt="GitHub issues">
    </a>
    <a href="https://github.com/izeleam/securenginx/stargazers">
        <img src="https://img.shields.io/github/stars/izeleam/securenginx?style=social" alt="GitHub stars">
    </a>
    <a href="https://github.com/izeleam/securenginx/network">
        <img src="https://img.shields.io/github/forks/izeleam/securenginx" alt="GitHub forks">
    </a>
    <br><br>
    <img src="https://raw.githubusercontent.com/izeleam/secure_nginx/.github/secure_nginx_logo.png" alt="Icon">
</p>

## Table of contents
- [Overview](#overview)
- [Quickstart](#quickstart)
- [Placeholders](#placeholders)
- [Security recommendations](#security-recommendations)
- [Notes & disclaimers](#notes--disclaimers)
- [Contributing](#contributing)
- [Quick links](#quick-links)

## Overview

This repository contains a curated set of NGINX configuration templates intended for learning and bootstrapping secure NGINX setups. The templates include examples for:

- Global `nginx.conf` defaults
- `conf.d` default catch-all with TLS hardening
- phpMyAdmin site configuration
- Generic reverse-proxy for apps (Node, Python, Go)
- Simple redirect site
- Static site hosting

Each template includes explanatory comments, sensible secure defaults and placeholders to make customization straightforward.

## Quickstart

1. Copy the template you need into your server's NGINX layout. Examples:

```bash
# copy global config (adapt carefully!)
sudo cp templates/nginx.conf.template /etc/nginx/nginx.conf

# copy site config and enable it
sudo cp templates/sites/phpmyadmin.conf.template /etc/nginx/sites-available/phpmyadmin.conf
sudo ln -s /etc/nginx/sites-available/phpmyadmin.conf /etc/nginx/sites-enabled/

# test and reload
sudo nginx -t
sudo systemctl reload nginx
```

2. Replace placeholders in the templates before testing:

- `{{SERVER_NAME}}`, `{{SSL_CERT}}`, `{{SSL_KEY}}`, `{{PHP_FPM_SOCKET}}`, etc.
- You can use a simple search/replace tool, a templating engine, or an editor.

## Placeholders

- `{{SERVER_NAME|example.com}}` — domain or host for the server block.
- `{{SSL_CERT}}` / `{{SSL_KEY}}` — TLS certificate and private key (e.g., Let's Encrypt paths).
- `{{PHP_FPM_SOCKET}}` — e.g., `unix:/var/run/php/php8.2-fpm.sock` or `127.0.0.1:9000`.
- `{{UPSTREAM_URL}}` — upstream app address like `http://127.0.0.1:3000`.

See `docs/USAGE.md` for more examples and testing with Docker.

## Security recommendations

- Keep TLS protocols to TLSv1.2+ and prefer strong cipher suites.
- Use Let's Encrypt certificates or a CA you control.
- Protect administrative interfaces (phpMyAdmin) behind IP allowlists, VPN or additional authentication.
- Monitor logs and enable automatic certificate renewal (`certbot renew`).
- Use `ssl_dhparam` with a strong group and enable OCSP stapling for better TLS performance.

## Notes & disclaimers

- These files are educational and should be adapted to your environment before production use.
- Paths like `/etc/letsencrypt/...` and PHP-FPM sockets are examples — verify them on your host.

## Contributing

Contributions are welcome — see `CONTRIBUTING.md` for the PR process, testing tips and style guidelines.

## Quick links

- Detailed usage and examples: `docs/USAGE.md`
- Security policy: `SECURITY.md`
