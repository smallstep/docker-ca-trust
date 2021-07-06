# docker-ca-trust

This is a set of Dockerfiles that can bootstrap an internal [`step-ca`](https://github.com/smallstep/certificates/) server on top of an OS image.
It can serve as a pattern for trusting internal CAs, for any Docker image.

Supported base images:

* `ubuntu:focal`
* `alpine:latest`

## Example usage

Say we want the `mongo` image to trust an internal CA.  `mongo` uses `ubuntu:focal`. So start with `Dockerfile.ubuntu`, and change `FROM ubuntu:focal` to `FROM mongo`. Build it and you will get a MongoDB server that trusts your CA.

The CA URL and Fingerprint can be hardcoded in the `Dockerfile`, or supplied as build arguments:

```
docker build -f Dockerfile.ubuntu . --build-arg CA_URL=https://ca.example.com --build-arg CA_FINGERPRINT=abc123123
docker build -f Dockerfile.alpine . --build-arg CA_URL=https://ca.example.com --build-arg CA_FINGERPRINT=abc123123
```

