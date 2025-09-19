Contributing to SecureNginx

Thanks for considering a contribution! This document explains how to contribute, code style, testing and the PR process.

How to contribute

1. Fork the repository and create a feature branch named `feat/your-topic` or `fix/your-topic`.
2. Make small, focused changes and include tests if applicable.
3. Open a Pull Request with a clear description and link to any relevant issues.

Testing and validation

- Templates should be validated locally with `nginx -t` after rendering placeholders.
- Example quick check using Docker (no root required):

```bash
# Render template into a temp dir and test with an nginx container
docker run --rm -v $(pwd)/tests/nginx-test:/etc/nginx:ro nginx:stable nginx -t
```

Code style

- Keep configuration comments clear and in English.
- Use placeholders of the form `{{NAME|default}}` in templates.

Pull Request checklist

- [ ] My changes are documented in README or the appropriate template header.
- [ ] I have linted and tested my changes locally.
- [ ] I have added or updated examples if applicable.

Maintainers will review and merge when changes pass CI and review.
