# ❌ Attempt 3

Use Docker provider and labels for configuration, but don't use an intermediate reverse proxy.

## Walkthrough

To test this, start up everything and tail logs with

```bash
docker compose up
```

Something like this will show up in `docker compose logs`:

```text
main-rproxy-1    | 2024-10-15T01:30:30Z WRN Could not find network named "web" for container "/simpler-isolator-whoami-1". Maybe you're missing the project's prefix in the label? container=whoami-simpler-isolator-3661ae0b044e8e4ae2f6c3be393f1b3b1ed8185e353d98a8e56e11468537529f providerName=docker serviceName=whoami-simpler-isolator
main-rproxy-1    | 2024-10-15T01:30:30Z WRN Defaulting to first available network (&{"private" "192.168.240.3" '\x00' "" "91912e10b43d57ff6571281a986f58c5f835faac9486ac035aee59898c3dc32f"}) for container "/simpler-isolator-whoami-1". container=whoami-simpler-isolator-3661ae0b044e8e4ae2f6c3be393f1b3b1ed8185e353d98a8e56e11468537529f providerName=docker serviceName=whoami-simpler-isolator
main-rproxy-1    | 2024-10-15T01:30:30Z ERR error="service \"whoami-simpler-isolator\" error: port is missing" container=whoami-simpler-isolator-3661ae0b044e8e4ae2f6c3be393f1b3b1ed8185e353d98a8e56e11468537529f providerName=docker
```
