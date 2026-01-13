# zscaler-cert

Zscaler's [public certificate](https://raw.githubusercontent.com/cfpb/zscaler-cert/refs/heads/main/zscaler_root_ca.pem) for your [application-specific trust store](https://help.zscaler.com/zia/adding-custom-certificate-application-specific-trust-store).

## What is `ca_bundle_with_zscaler.pem`?

I took [Mozilla's CA certificate store](https://curl.se/docs/caextract.html) and added the Zscaler root CA signature to the bottom of it. Some projects might want a full list of certificate authorities.
