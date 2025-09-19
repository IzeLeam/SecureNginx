USAGE — SecureNginx Templates

Purpose

This document expands on README instructions with concrete examples for beginners and experts.

Quickstart

1. Choose a template from `templates/sites/`.
2. Copy to your server's nginx layout and replace placeholders. Example:

```bash
sudo cp templates/sites/phpmyadmin.conf.template /etc/nginx/sites-available/phpmyadmin.conf
sudo ln -s /etc/nginx/sites-available/phpmyadmin.conf /etc/nginx/sites-enabled/
# Edit /etc/nginx/sites-available/phpmyadmin.conf and set SERVER_NAME, SSL paths, PHP_FPM_SOCKET
sudo nginx -t
sudo systemctl reload nginx
```

Placeholder guide

- `{{SERVER_NAME|example.com}}` — replace with your domain.
- `{{SSL_CERT}}` / `{{SSL_KEY}}` — fullchain and private key paths (Let's Encrypt example provided in templates).
- `{{PHP_FPM_SOCKET}}` — e.g., `unix:/var/run/php/php8.2-fpm.sock` or `127.0.0.1:9000`.
- `{{UPSTREAM_URL}}` — e.g., `http://127.0.0.1:3000` for apps.

Testing with Docker (safe local validation)

1. Render templates into a temporary directory (replace placeholders first).
2. Run:

```bash
docker run --rm -v $(pwd)/tmp-nginx:/etc/nginx:ro nginx:stable nginx -t -c /etc/nginx/nginx.conf
```

Best practices

- Use `ssl_dhparam` with at least 4096-bit groups for ephemeral DH.
- Use HSTS (`Strict-Transport-Security`) carefully if you own the domain.
- Restrict admin panels with `allow`/`deny` or basic auth.
- Enable OCSP stapling for better TLS performance.

Contributing

See `CONTRIBUTING.md` for PR process, tests and local validation tips.
