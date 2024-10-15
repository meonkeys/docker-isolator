# ✅ Attempt 1

Isolation without the 2nd reverse proxy used in Attempt 2.

Must use Traefik file provider.

## Walkthrough

To test this, start up everything and tail logs with

```bash
docker compose up
```

This starts up three containers.

1. `main-rproxy` - Traefik. Highly trusted, kept up to date, etc. Imagine this service exposed on a WAN (via a router port-forwarding to it). Excludes HTTPS for simplicity. [Source](https://github.com/traefik/traefik/).
1. `whoami` - Simulated untrusted or less-trustworthy service. [Source](https://github.com/traefik/whoami).
1. `jailed-worker` - Simulated companion/sidecar to the untrusted or less-trustworthy service. Exists to provide a network sandbox for testing because `whoami` is a refreshingly minimal image (without even a shell). [Source](https://github.com/nicolaka/netshoot).

In a separate terminal, try:

```bash
curl -v http://whoami.docker.localhost
```

## See also

* Experiment further in `../Readme.md`
