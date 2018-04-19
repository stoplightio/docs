# Configuring SAML Authentication

To configure Stoplight Enterprise to use SAML for user authentication,
add the following variable to the Stoplight API
configuration/environment:

```bash
SL_SSO_ENTRYPOINT="https://your-saml-server.example.com/..."
```

Where `SL_SSO_ENTRYPOINT` is the full URL to the SAML server providing
the SAML assertions.

Once set in the API configuration, restart the API:

```bash
# docker installs
sudo docker restart stoplight-api

# package installs
sudo systemctl restart stoplight-api
```

Once restarted, all login requests will be authenticated via the
external SAML service.

> Please note, Stoplight's SAML integration does not currently use
  SAML assertions for determining group/organization
  membership. Group/organization membership should be managed through
  the Stoplight application itself.

## SAML IdP Metadata

To configure Stoplight SAML integration from the SAML server, use the following SAML metadata file:

```xml
<EntityDescriptor xmlns="urn:oasis:names:tc:SAML:2.0:metadata" xmlns:ds="http://www.w3.org/2000/09/xmldsig#" entityID="stoplight" ID="stoplight">
<SPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
<NameIDFormat>
urn:oasis:names:tc:SAML:2.0:nameid-format:persistent
</NameIDFormat>
<AssertionConsumerService index="1" isDefault="true" Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST" Location="https://stoplight-api.internal.example.com/sso/global/saml/callback"/>
</SPSSODescriptor>
</EntityDescriptor>
```

Be sure to update the `AssertionConsumerService` / `Location` object
with the correct callback URL for the Stoplight API.