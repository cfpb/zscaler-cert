# zscaler-cert

Zscaler's [public certificate](https://raw.githubusercontent.com/cfpb/zscaler-cert/refs/heads/main/zscaler_root_ca.pem) (also available as a [DER binary file](https://raw.githubusercontent.com/cfpb/zscaler-cert/refs/heads/main/zscaler_root_ca.cer)) for your [application-specific trust store](https://help.zscaler.com/zia/adding-custom-certificate-application-specific-trust-store).

## Docker and Zscaler

If you're using Docker in a project, you'll need to add this to your Dockerfile:

```
ADD https://raw.githubusercontent.com/cfpb/zscaler-cert/refs/heads/main/zscaler_root_ca.pem /usr/local/share/ca-certificates/zscaler_root_ca.crt
RUN update-ca-certificates
```

If your base image doesn't include certificate management tooling, you'll do something like:

```
ADD https://raw.githubusercontent.com/cfpb/zscaler-cert/refs/heads/main/zscaler_root_ca.pem /usr/local/share/ca-certificates/zscaler_root_ca.crt
RUN apk add --no-cache --no-check-certificate ca-certificates && \
    update-ca-certificates &&
```

If npm is failing, you might have to:

```
ENV NODE_EXTRA_CA_CERTS=/etc/ssl/certs/ca-certificates.crt
```

Here's how it looks in consumerfinance.gov's [`Dockerfile`](https://github.com/cfpb/consumerfinance.gov/compare/ZsCaLeR).

## What is `ca_bundle_with_zscaler.pem`?

I took [Mozilla's CA certificate store](https://curl.se/docs/caextract.html) and added the Zscaler root CA signature to the bottom of it. Some projects might want a full list of certificate authorities.
