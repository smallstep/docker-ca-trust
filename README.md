# docker-ca-trust

This is an example of a Docker image that bootstraps with an internal `step-ca` server.
It can serve as a pattern for trusting internal CAs, for any Ubuntu-based Docker image.
The CA URL and Fingerprint can be hardcoded in the `Dockerfile` or supplied as build arguments.

This image can be layered on top of any Ubuntu-based server image.
For example, change `FROM ubuntu:focal` to `FROM mongo` and you will get a MongoDB server that trusts your CA.
The CA certificate is stored in `/usr/local/share/ca-certificates/root_ca.crt` in the container.

To build it:

```
docker build . --build-arg CA_URL=https://ca.smallstep.com --build-arg CA_FINGERPRINT=abc123123
```

