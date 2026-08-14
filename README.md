# OpenID Connect (OIDC) Authentication with Okta

## Overview

This project demonstrates the implementation of OpenID Connect (OIDC) authentication using Okta as the Authorization Server and Identity Provider (IdP). The lab focuses on understanding the underlying mechanics of the OIDC Authorization Code Flow, including authentication requests, authorization code generation, redirect behavior, token exchange, and token issuance.

Unlike a traditional application integration, this project intentionally isolates the protocol itself. Rather than developing a client application to complete the flow, the authorization code was manually obtained and exchanged for tokens using Postman. This approach provided visibility into each stage of the authentication process and a deeper understanding of how modern authentication protocols operate.

OIDC is built on top of OAuth 2.0 and provides a standardized method for verifying user identities while securely delivering identity information to applications.

---

## Architecture

The authentication flow follows the process below:

1. A user attempts to log in to an application.
2. The client application sends an authentication request to Okta.
3. The request includes metadata such as scopes, redirect URI, response type, and client information.
4. Okta authenticates the user.
5. Okta generates an Authorization Code.
6. Okta redirects the user back to the configured Redirect URI.
7. The client exchanges the Authorization Code at Okta's Token Endpoint.
8. Okta validates the request and issues tokens containing user claims.
9. The application validates the tokens and establishes an authenticated session.

---

## Technologies Used

| Technology                        | Purpose                                  |
| --------------------------------- | ---------------------------------------- |
| Okta Identity Engine              | Authorization Server / Identity Provider |
| OpenID Connect (OIDC)             | Authentication Protocol                  |
| OAuth 2.0 Authorization Code Flow | Token Exchange Framework                 |
| Postman                           | Token Exchange Testing                   |
| ID Tokens                         | User Identity Information                |
| Access Tokens                     | API Authorization                        |
| Claims                            | User Attributes Within Tokens            |

---

## Key IAM Concepts Demonstrated

### Authorization Server / Identity Provider

Okta serves as both the Authorization Server and Identity Provider.

Responsibilities include:

* Authenticating users
* Managing login sessions
* Issuing authorization codes
* Generating tokens
* Providing identity information
* Enforcing authentication policies

Okta acts as the trusted authority responsible for validating user identities and issuing tokens to applications.

---

### Authentication Request

The authentication process begins when a client application redirects a user to Okta.

The request contains metadata such as:

* Client ID
* Redirect URI
* Response Type
* Requested Scopes
* State Parameter
* Nonce Value

Example scopes:

```text
openid
profile
email
```

The `openid` scope identifies the request as an OpenID Connect authentication request.

---

### User Authentication

After receiving the authentication request, Okta authenticates the user using configured authentication methods.

Examples include:

* Username and Password
* Multi-Factor Authentication (MFA)
* Passwordless Authentication
* Adaptive Authentication Policies

Once authentication succeeds, Okta creates a session and continues the authorization process.

---

### Authorization Code

After successful authentication, Okta generates an Authorization Code.

The Authorization Code is:

* Temporary
* Short-lived
* Single-use
* Not directly usable for API access

The Authorization Code serves as an intermediary credential that can later be exchanged for tokens.

---

### Redirect URI

The Redirect URI is a trusted endpoint registered within Okta.

After successful authentication, Okta redirects the browser to the configured Redirect URI and appends the Authorization Code as a query parameter.

Example:

```text
https://sample-app.com/callback?code=AUTHORIZATION_CODE
```

Only preconfigured Redirect URIs are allowed, helping prevent unauthorized token delivery.

---

### Authorization Code Flow Validation

This project intentionally focused on understanding the protocol rather than building a fully functional client application.

A sample Redirect URI was configured within Okta, but no actual application existed at that location.

The authentication flow behaved as expected:

1. Okta authenticated the user.
2. Okta redirected the browser to the configured Redirect URI.
3. The redirect destination did not exist.
4. The browser URL still contained the generated Authorization Code as a query parameter.

Because the Authorization Code is expected to travel through the user's browser, the code remained visible within the URL even though the destination application was unavailable.

The Authorization Code was then manually extracted from the browser URL for testing purposes.

This allowed the remainder of the OIDC flow to be validated without building a custom client application.

---

### Token Exchange

In production environments, the Authorization Code is typically exchanged by a backend application.

The backend sends a secure request to Okta's Token Endpoint containing:

* Authorization Code
* Client Credentials
* Redirect URI

Okta validates the request and returns tokens.

For this lab, Postman was used to simulate the backend application.

The Authorization Code obtained from the browser URL was manually submitted to Okta's Token Endpoint, successfully completing the Authorization Code Flow and validating the token exchange process.

This approach provided direct visibility into how applications obtain tokens from an Authorization Server.

---

### Why Token Exchange Happens on the Backend

A key security principle of OIDC is that Authorization Codes may travel through the browser, while token acquisition should occur through a secure back-channel connection.

Authorization Code:

```text
Browser
   │
   ▼
Authorization Code
```

Token Exchange:

```text
Backend Application
   │
   │ POST /token
   ▼
Okta Token Endpoint
   │
   ▼
ID Token
Access Token
```

Keeping token exchanges on the backend helps protect sensitive credentials and reduces exposure of tokens within the browser.

---

### Tokens

After validating the Authorization Code, Okta issues tokens to the client.

#### ID Token

The ID Token contains identity information about the authenticated user.

Examples:

* User ID
* Name
* Email Address
* Authentication Time
* Session Information

The ID Token allows applications to verify user identity.

#### Access Token

The Access Token is used to authorize requests to protected APIs and resources.

The token represents permissions granted during authentication.

---

### Claims

Claims are pieces of identity information contained within tokens.

Examples include:

* Subject Identifier (sub)
* Name
* Email
* Preferred Username
* Groups
* Roles
* Custom Attributes

Applications use claims to personalize experiences and make authorization decisions.

---

### Authentication vs Authorization

This project highlights the distinction between authentication and authorization.

#### Authentication

Authentication answers:

> Who is the user?

Okta performs authentication by validating the user's identity.

#### Authorization

Authorization answers:

> What is the user allowed to access?

Applications use token claims to determine permissions and access levels.

---

## OIDC Authorization Code Flow

```text
User
 │
 ▼
Client Application
 │
 │ Authentication Request
 │ (openid, profile, email)
 ▼
Okta Authorization Server
 │
 │ User Authentication
 ▼
Authorization Code Issued
 │
 ▼
Redirect URI
 │
 ▼
Authorization Code Retrieved
 │
 ▼
Postman (Client Simulation)
 │
 │ POST /token
 ▼
Okta Token Endpoint
 │
 ▼
ID Token + Access Token
 │
 ▼
Token Validation
 │
 ▼
Access Granted
```

---

## Skills Demonstrated

* Identity and Access Management (IAM)
* OpenID Connect (OIDC)
* OAuth 2.0 Authorization Code Flow
* Modern Authentication Protocols
* Authentication Architecture
* Authorization Concepts
* Token-Based Authentication
* Claims Management
* Redirect URI Configuration
* Authorization Server Configuration
* Postman API Testing
* Okta Administration
* Identity Federation Fundamentals

---

## Learning Outcomes

By completing this project, I gained hands-on experience implementing and validating the OpenID Connect Authorization Code Flow using Okta.

Rather than relying on a prebuilt application, this lab exposed the underlying mechanics of the protocol, including authentication requests, authorization code generation, redirect URI behavior, token endpoint interactions, and token issuance.

Using Postman to manually exchange the Authorization Code provided a deeper understanding of how applications securely obtain tokens from an Authorization Server and how identity information is delivered through claims contained within those tokens.

This project mirrors the authentication architecture used by modern cloud applications, SaaS platforms, and enterprise identity ecosystems.
