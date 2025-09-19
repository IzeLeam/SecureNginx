SecureNginx - Educational NGINX Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Validate templates](https://github.com/IzeLeam/SecureNginx/actions/workflows/validate-templates.yml/badge.svg)](.github/workflows/validate-templates.yml)

Overview

This repository contains a curated set of NGINX configuration templates intended for learning and bootstrapping secure NGINX setups. The templates include examples for:
- Global `nginx.conf` defaults
- `conf.d` default catch-all with TLS hardening
- phpMyAdmin site configuration
- Generic reverse-proxy for apps (Node, Python, Go)
- Simple redirect site
- Static site hosting

How to use

1. Copy the template you need into your server's `/etc/nginx` layout. For example:
   - Copy `templates/nginx.conf.template` to `/etc/nginx/nginx.conf` and adapt placeholders.
   - Copy `templates/sites/phpmyadmin.conf.template` to `/etc/nginx/sites-available/phpmyadmin.conf` and create a symlink in `sites-enabled`.

2. Replace placeholders:
   - `{{SERVER_NAME}}`, `{{SSL_CERT}}`, `{{SSL_KEY}}`, `{{PHP_FPM_SOCKET}}`, etc.
   - You can use a simple search/replace tool or template engine.

3. Test and reload:
   - Run `nginx -t` to check syntax.
   - Reload: `systemctl reload nginx`.

Security recommendations

- Keep TLS protocols to TLSv1.2+ and prefer strong cipher suites.
- Use Let's Encrypt certificates or a CA you control.
- Protect administrative interfaces (phpMyAdmin) behind IP allowlists or additional auth.
- Monitor logs and enable automatic certificate renewal.

Notes and disclaimers

- These files are educational and should be adapted to your environment before production use.
- Paths like `/etc/letsencrypt/...` and PHP-FPM sockets are examples.

Contributing

- Open PRs with improvements or additional templates. See `CONTRIBUTING.md` for details.

Quick links

- Detailed usage and examples: `docs/USAGE.md`
- Security policy: `SECURITY.md`
- Code of Conduct: `CODE_OF_CONDUCT.md`

