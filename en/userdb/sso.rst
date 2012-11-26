
Dream authentication service
****************************

Dream authentication service provides 3rd party services the way to
identify, authenticate and authorize users in the Dream platform.

Each service can register service specific permissions to the UserDB.
These permissions are then provided to the service when user logs in
to the system.

All services can authenticate all users, and it is the responsibility
of the service to check if the user should have access to the service
or not and what actions the user can do inside the service.

The service can use only data provided back in authentication requests
as attributes. Or the service can request access to the UserDB API to
query data directly from the database.

SAML v2 Identity Provider
=========================

SSO
  Single sign on service https://id.dreamschool.fi/saml/SSO/
SLO
  Single log out service: https://id.dreamschool.fi/saml/SLO/
Metadata
  https://id.dreamschool.fi/saml/metadata/

SLO can be initiated by using RelayState GET-parameter with SLO URL:
https://id.dreamschool.fi/saml/SLO/?RelayState=http://kasavuori.fi

Attributes
==========

The SAML response has basic user information included.
List of available attributes:

givenName
  "teppo"
familyName
  "testaaja"
name
  "testatep"
organisations
  ["1", "2"] (unique ids)
roles
  ["1.1", "2.1"] (unique ids)
permissions
  ["dsuserdb.service.api", "dscms.article.add"] (unique ids)
locale
  "fi-fi"

Attributes can be present with the names listed above, or their absolute
object identifier format. For example ``givenName`` can be ``urn:oid:2.5.4.42``.

All attributes are strings. Attribute name and items in
lists organisations, roles and permissions are unique.

Roles are in the format ``<organisation>.<role>``.

Example config for SimpleSAMLphp
================================

metadata/saml20-idp-remote.php
------------------------------

::

  $metadata['id.dreamschool.fi'] = array (
    'entityid' => 'id.dreamschool.fi',
    'contacts' =>
    array (
    ),
    'metadata-set' => 'saml20-idp-remote',
    'SingleSignOnService' =>
    array (
      0 =>
      array (
        'Binding' => 'urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect',
        'Location' => 'https://id.dreamschool.fi/saml/SSO/',
      ),
    ),
    'SingleLogoutService' =>
    array (
      0 =>
      array (
        'Binding' => 'urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect',
        'Location' => 'https://id.dreamschool.fi/saml/SLO/',
      ),
    ),
    'ArtifactResolutionService' =>
    array (
    ),
    'keys' =>
    array (
      0 =>
      array (
        'encryption' => false,
        'signing' => true,
        'type' => 'X509Certificate',
        'X509Certificate' => 'MIIEDDCCAvSgAwIBAgIJAJIy7M+uXf/3MA0GCSqGSIb3DQEBBQUAMGExCzAJBgNVBAYTAkZJMRAwDgYDVQQIEwdUYW1wZXJlMRAwDgYDVQQHEwdUYW1wZXJlMREwDwYDVQQKEwhIYWx0dSBPeTEbMBkGA1UEAxMSd3d3LmRyZWFtc2Nob29sLmZpMB4XDTExMDIwMTEyNTMyNFoXDTIxMDEzMTEyNTMyNFowYTELMAkGA1UEBhMCRkkxEDAOBgNVBAgTB1RhbXBlcmUxEDAOBgNVBAcTB1RhbXBlcmUxETAPBgNVBAoTCEhhbHR1IE95MRswGQYDVQQDExJ3d3cuZHJlYW1zY2hvb2wuZmkwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC335M1JHBAiWEpLB6FAKTS5ZhxCoyfY/1uEG814iSUYozFPi6vm5H2GsCj2vJeNYoMhUltG0Q0FWjJMVolU2cSVcHpXnfavie816UsiAT/h6825btdxE5c8IsZ913ChSfBZ1sCOzS1v41Ox8wL66rOfRRpawYwEkXTL0kzuhrw9XgM4eTTj1q5uKx/55Hqc6sD17j2ehfpWrAhIYTPNJez8hps58YmctaJootiyy3fKS7LKUJG4VKaD1xW/imdEpbxLUhG314Zde/yyL8jRxcexDVXJIq/VXDvgLvPYIhR9cyOjj3cILN4ToJUaVIz6mA4nOeO1LOKb4CITh9D4rhXAgMBAAGjgcYwgcMwHQYDVR0OBBYEFCqc3t5HNxh34UiauH10iysWQzdSMIGTBgNVHSMEgYswgYiAFCqc3t5HNxh34UiauH10iysWQzdSoWWkYzBhMQswCQYDVQQGEwJGSTEQMA4GA1UECBMHVGFtcGVyZTEQMA4GA1UEBxMHVGFtcGVyZTERMA8GA1UEChMISGFsdHUgT3kxGzAZBgNVBAMTEnd3dy5kcmVhbXNjaG9vbC5maYIJAJIy7M+uXf/3MAwGA1UdEwQFMAMBAf8wDQYJKoZIhvcNAQEFBQADggEBAHFTfiOppPEou6f1mc88mlHuMpLSpfk++KS5cEJUWucGjGktRSjbNbzgyPmWEtYm8kYbqguaCHsqztIFjh/8ITZIwqS9nz22qikJVZAonWynN7fjXNWgKfqPKBclBi5b3BhhX5XYKoYjWQ0hmzTj6a8He91WeM/89h7YxEhq6bXwodqAW2s26LjkcZAFkarOdScCk6IISYX/oU/YM4802YHD0FGy8/S100wAsMcvL6Wc+PhJUF+/ZgxZKboF+k3pIyJs1LlFYetBnzeDrOmFDEIQzeq2dkPvjgJO7nlOpK3VYL2NwmcmfEzOvutnFeOYsHheq62XjPHdk7rl7fVkxSg=',
      ),
      1 =>
      array (
        'encryption' => true,
        'signing' => false,
        'type' => 'X509Certificate',
        'X509Certificate' => 'MIIEDDCCAvSgAwIBAgIJAJIy7M+uXf/3MA0GCSqGSIb3DQEBBQUAMGExCzAJBgNVBAYTAkZJMRAwDgYDVQQIEwdUYW1wZXJlMRAwDgYDVQQHEwdUYW1wZXJlMREwDwYDVQQKEwhIYWx0dSBPeTEbMBkGA1UEAxMSd3d3LmRyZWFtc2Nob29sLmZpMB4XDTExMDIwMTEyNTMyNFoXDTIxMDEzMTEyNTMyNFowYTELMAkGA1UEBhMCRkkxEDAOBgNVBAgTB1RhbXBlcmUxEDAOBgNVBAcTB1RhbXBlcmUxETAPBgNVBAoTCEhhbHR1IE95MRswGQYDVQQDExJ3d3cuZHJlYW1zY2hvb2wuZmkwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC335M1JHBAiWEpLB6FAKTS5ZhxCoyfY/1uEG814iSUYozFPi6vm5H2GsCj2vJeNYoMhUltG0Q0FWjJMVolU2cSVcHpXnfavie816UsiAT/h6825btdxE5c8IsZ913ChSfBZ1sCOzS1v41Ox8wL66rOfRRpawYwEkXTL0kzuhrw9XgM4eTTj1q5uKx/55Hqc6sD17j2ehfpWrAhIYTPNJez8hps58YmctaJootiyy3fKS7LKUJG4VKaD1xW/imdEpbxLUhG314Zde/yyL8jRxcexDVXJIq/VXDvgLvPYIhR9cyOjj3cILN4ToJUaVIz6mA4nOeO1LOKb4CITh9D4rhXAgMBAAGjgcYwgcMwHQYDVR0OBBYEFCqc3t5HNxh34UiauH10iysWQzdSMIGTBgNVHSMEgYswgYiAFCqc3t5HNxh34UiauH10iysWQzdSoWWkYzBhMQswCQYDVQQGEwJGSTEQMA4GA1UECBMHVGFtcGVyZTEQMA4GA1UEBxMHVGFtcGVyZTERMA8GA1UEChMISGFsdHUgT3kxGzAZBgNVBAMTEnd3dy5kcmVhbXNjaG9vbC5maYIJAJIy7M+uXf/3MAwGA1UdEwQFMAMBAf8wDQYJKoZIhvcNAQEFBQADggEBAHFTfiOppPEou6f1mc88mlHuMpLSpfk++KS5cEJUWucGjGktRSjbNbzgyPmWEtYm8kYbqguaCHsqztIFjh/8ITZIwqS9nz22qikJVZAonWynN7fjXNWgKfqPKBclBi5b3BhhX5XYKoYjWQ0hmzTj6a8He91WeM/89h7YxEhq6bXwodqAW2s26LjkcZAFkarOdScCk6IISYX/oU/YM4802YHD0FGy8/S100wAsMcvL6Wc+PhJUF+/ZgxZKboF+k3pIyJs1LlFYetBnzeDrOmFDEIQzeq2dkPvjgJO7nlOpK3VYL2NwmcmfEzOvutnFeOYsHheq62XjPHdk7rl7fVkxSg=',
      ),
    ),
  );

Registering your service
========================

When you want to use the IdP for single sign on in a Dream
service you need to provide your assertion consumer service and
single log out service endpoint URLs to us.

Contact Haltu for your service registration.

Information from SimpleSAMLphp
------------------------------

When using SimpleSAMLphp the information you need to provide looks
something like this::

  $metadata['http://movies.dreamschool.fi/simplesaml/module.php/saml/sp/metadata.php/default-sp'] = array(
    'AssertionConsumerService' => 'http://movies.dreamschool.fi/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp',
    'SingleLogoutService' => 'http://movies.dreamschool.fi/simplesaml/module.php/saml/sp/saml2-logout.php/default-sp',
  );


