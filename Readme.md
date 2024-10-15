# Docker service isolation demos

Demonstrate different approaches to web service network isolation using only Docker Compose.

Goals:

* Stand up a `whoami` service.
* Allow proxied access to the service.
* Block all outbound access from the service.

`whoami` is a stand-in for any service that doesn't need outbound (e.g. Internet) access.

These attempts cannot be run simultaneously.

## ✅ Attempt 1: file provider, no intermediate proxy

The simplest solution is to avoid the Traefik [docker provider](https://doc.traefik.io/traefik/providers/docker/) and use the [file provider](https://doc.traefik.io/traefik/providers/file/) instead.

See `attempt-01/Readme.md`.

## ✅ Attempt 2: docker provider, intermediate proxy

This works and has different characteristics than Attempt 1.

See `attempt-02/Readme.md`.

## ❌ Attempt 3: docker provider, no intermediate proxy

This doesn't appear to work.

See `attempt-03/Readme.md`.

## Experiment further

Here are some additional things to try once you have a working attempt running.

### Traefik dashboard

See the Traefik dashboard on the host at <http://localhost:8080>.

### ping tests

To test network access from within the `private` (isolated) network, run

```bash
docker compose exec jailed-worker bash
```

Now you're in a [netshoot](https://github.com/nicolaka/netshoot) container. Try:

```bash
# should succeed
ping whoami

# should fail outright / hang
ping web

# DNS query should work, actual ping should hang
ping adammonsen.com
```

## See also

* [filter outbound container network traffic : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/1f5vqqn/filter_outbound_container_network_traffic/)
* [Restrict Internet Access - Docker Container - Stack Overflow](https://stackoverflow.com/questions/39913757/restrict-internet-access-docker-container)
* [Preventing egress / outbound traffic from container, except via sidecar gateway/proxy - Nomad - HashiCorp Discuss](https://discuss.hashicorp.com/t/preventing-egress-outbound-traffic-from-container-except-via-sidecar-gateway-proxy/56488)
* [linux - Docker: Restricting inbound and outbound traffic using iptables - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/628827/docker-restricting-inbound-and-outbound-traffic-using-iptables)
* [Restrict Internet Access - Docker Container - Stack Overflow](https://stackoverflow.com/questions/39913757/restrict-internet-access-docker-container)

## FAQ

Why?
: I wanted a way to block outbound traffic from containers without modifying images and without having to work with iptables.

Why Traefik?
: Just happens to be something I'm familiar with.

Why Nginx?
: It's a popular reverse proxy and it looked easy to set up. It was.

Why not iptables?
: Looks hard. I'm not super confident with it.

What about web sockets?
: I don't know. Maybe that'll work as-is, or with a few more lines of Nginx config?

What about HTTPS?
: I was assuming Traefik would terminate HTTPS traffic, so Nginx and the isolated service shouldn't need to handle that.

How do I get real client IP addresses with multiple reverse proxies?
: I don't know. Should be doable with the right headers.

## Copyright and license

This demonstration is (C)2024 Adam Monsen.
Some rights reserved.
License is [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) License](https://creativecommons.org/licenses/by-sa/4.0/).
