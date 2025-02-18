---
title: 'Access control - authentication overview'
sidebar_label: 'Authentication overview'
id: authentication-overview
keywords: [server, access control, authentication, overview]
tags:
  - server
  - access control
  - authentication
  - overview
---


Your application can perform authentication through many techniques. All these techniques support [Multi-factor Authentication (MFA)](https://en.wikipedia.org/wiki/Multi-factor_authentication) to bring additional security.

You can set Username and Password authentication to use one of three solutions:

* INTERNAL
* LDAP
* HYBRID

SSO authentication is further broken down into one of the following:

* [JWT (JSON Web Token)](https://jwt.io/introduction) SSO
* [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language)
* [OIDC](https://openid.net/connect/)

Each of these requires its own configuration settings in the application's _application-name-_**auth-preferences.kts** file. And within that file, all the configuration settings mudt be wrapped in a single `security` function.

## Username and password authentication

Username and password authentication allow users to log in directly to your application. You must choose one of the provided solutions in order control this process.

To specify which one to use, just edit the application's **auth-preferences.kts** file and change the `type` variable in the `authentication` block to match the required value. For example:

```kotlin
security {
  authentication {
    type = AuthType.LDAP
  }
}
```

:::note

If you do not specify an authentication type, INTERNAL authentication is used.

:::

The three values that this can be set to are:

* AuthType.INTERNAL
* AuthType.LDAP
* AuthType.HYBRID

The differences between the solutions associated with each value are detailed below.

### Internal

Internal authentication uses internally stored hashed credentials to authenticate users. It checks user credentials against an internal table. 

Internal authentication provides the following features:

- User accounts can be locked
- Passwords can be set to expire
- Passwords can be required to conform to a configurable standard
- Users can reset or change their password (assuming they can log in first)

Internal authentication is the default authentication behaviour if you don't specify a `type` in **auth-preferences.kts**.

```kotlin
    authentication {
        type = AuthType.INTERNAL
    }
```

### LDAP

LDAP authentication uses its namesake protocol to authenticate users. 

LDAP authentication relies on an external party that cannot be operated from your application. So, by setting LDAP, you lose control of the internal authentication functionality. As a direct consequence, requests to change or reset passwords won't be accepted.

For LDAP authentication, a username must exist inside the internal records of the application. To do this, create a user entry inside the USER table for every LDAP user of the application. There is no password checking between this login and the application's internal records; authentication will rely solely on LDAP.

To set up LDAP authentication, a connection to an LDAP server must be configured in the **auth-preferences.kts** file.

For more information on configuring LDAP authentication, see [Username and password authentication](../../../server/access-control/password-authentication/#authentication).

The example below shows LDAP authentication specified, with `userIdType` set to `cn` for the search for the username.

```kotlin
    authentication {
        type = AuthType.LDAP
		ldap {
		    connection {
		        url = "localhost"
                port = 389
                searchBases {
				    searchBase {
                        entry("ou=People,dc=example,dc=com")
			        }
                }
                bindDn = "CN=DTADevBindUser,ou=People,dc=example,dc=com"
                bindPassword = "password123"
                userIdType = "cn"	
			}
		}
    }
```

### Hybrid

As its name suggests, hybrid mode is a mix of Internal and LDAP authentication modes, and it checks credentials against both.

First, an internal authentication is performed. If the outcome is successful, further authentication is then performed against the LDAP server. The login request is only successful if both authentications are successful.

This enables you to take advantage of all the available functionality of internal mode (locked accounts, expiring passwords, reset/change passwords). However, if passwords are changed or expired, they need to be changed manually in LDAP too, because authentication always happens in both services.

The configuration file takes the same fields as LDAP. You can see this in the example below, where the authentication `type` has been set to `HYBRID`.

```kotlin
    authentication {
        type = AuthType.HYBRID
        ldap {
		    connection {
		        url = "localhost"
                port = 389
                searchBases {
				    searchBase {
                        entry("ou=People,dc=example,dc=com")
			        }
                }
                bindDn = "CN=DTADevBindUser,ou=People,dc=example,dc=com"
                bindPassword = "password123"
                userIdType = "cn"	
			}
		}
    }
```

## SSO authentication

SSO authentication enables users to use a single set of credentials to access a range of applications, including those built on the Genesis low-code platform. For more information on SSO technology, please visit the [Single-sign on Wikipedia page](https://en.wikipedia.org/wiki/Single_sign-on).

SSO authentication is a more involved process to enable; it requires additional file changes, which are detailed in the following pages:

- [SSO - JWT](../../../server/access-control/SSO-jwt/)
- [SSO - SAML](../../../server/access-control/SSO-saml/)
- [SSO - OIDC](../../../server/access-control/SSO-oidc/)

Both SSO and password authentication can be used concurrently by applications built on the platform; the use of one does not mandate nor prevent the use of the other.
