# OpenID Connect (OIDC) Authentication with Okta

## Overview

This project demonstrates the implementation of OpenID Connect (OIDC) authentication using Okta as the Authorization Server and Identity Provider (IdP), and a client application acting as the relying party.

The objective of this lab is to understand how modern applications authenticate users using the OIDC Authorization Code Flow. The project showcases how authentication requests are processed, how authorization codes are exchanged for tokens, and how identity information is securely transmitted through claims contained within tokens.

OIDC is built on top of OAuth 2.0 and provides a standardized method for verifying user identity while enabling secure access to applications.

---

## Architecture

The authentication flow follows the process below:

1. A user attempts to access an application.
2. The client application redirects the user to Okta for authentication.
3. The authentication request includes metadata such as client information, redirect URI, and requested scopes.
4. Okta authenticates the user.
5. Okta issues an authorization code and redirects the user back to the application.
6. The application exchanges the authorization code at Okta's token endpoint.
7. Okta validates the request and issues tokens.
8. The application validates the tokens and grants access to the user.

---

## Technologies Used

| Technology                        | Purpose                                  |
| --------------------------------- | ---------------------------------------- |
| Okta Identity Engine              | Authorization Server / Identity Provider |
| OpenID Connect (OIDC)             | Authentication Protocol                  |
| OAuth 2.0 Authorization Code Flow | Token Exchange Framework                 |
| Client Application                | Application requesting authentication    |
| ID Tokens                         | User identity information                |
| Access Tokens                     | API authorization                        |
| Claims                            | User attributes within tokens            |

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

Okta becomes the trusted authority responsible for validating user identities.

---

### Client Application

The client application initiates the authentication process when a user attempts to log in.

Responsibilities include:

* Redirecting users to Okta
* Sending authentication requests
* Receiving authorization codes
* Exchanging codes for tokens
* Validating tokens
* Establishing application sessions

Unlike traditional authentication methods, the application never directly handles user credentials.

---

### Authentication Request

The authentication process begins when the client sends an authorization request to Okta.

The request contains metadata such as:

* Client ID
* Redirect URI
* Response Type
* Requested Scopes
* State Parameter
* Nonce Value

Example requested scopes:

```text
openid
profile
email
```

The `openid` scope identifies the request as an OpenID Connect authentication request.

---

### User Authentication

After receiving the authentication request, Okta authenticates the user through configured authentication methods.

Examples include:

* Username and Password
* Multi-Factor Authentication (MFA)
* Passwordless Authentication
* Adaptive Authentication Policies

Once successful, Okta establishes the user's authenticated session.

---

### Authorization Code

Following successful authentication, Okta generates an authorization code.

The authorization code is:

* Temporary
* Short-lived
* Single-use
* Not directly usable by applications

The code is sent back to the client application's configured Redirect URI.

This mechanism prevents sensitive tokens from being exposed through the user's browser.

---

### Redirect URI

The Redirect URI is a trusted endpoint registered within Okta.

After authentication, Okta redirects the user back to this endpoint and includes the authorization code.

Only preconfigured Redirect URIs are allowed, helping prevent unauthorized token delivery.

---

### Token Exchange

Once the client receives the authorization code, it communicates directly with Okta's Token Endpoint.

The client submits:

* Authorization Code
* Client Credentials
* Redirect URI

The authorization code is exchanged for tokens through a secure back-channel communication.

This process is commonly referred to as the Authorization Code Flow.

---

### Tokens

After validating the authorization code request, Okta issues tokens to the client application.

Common tokens include:

#### ID Token

The ID Token contains identity information about the authenticated user.

Examples:

* User ID
* Name
* Email Address
* Authentication Time
* Session Information

The ID Token allows the application to verify who the user is.

#### Access Token

The Access Token is used to access protected APIs and resources.

The token represents the permissions granted during authentication.

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

Applications use claims to personalize user experiences and make authorization decisions.

---

### Authentication vs Authorization

This project highlights the distinction between authentication and authorization.

#### Authentication

Authentication answers:

> "Who is the user?"

Okta performs authentication by validating the user's identity.

#### Authorization

Authorization answers:

> "What is the user allowed to access?"

Applications use claims contained within tokens to determine permissions and access levels.

---

## OIDC Authorization Code Flow

```text id="3d4z9m"
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
Client Application
 │
 │ Authorization Code Exchange
 ▼
Okta Token Endpoint
 │
 ▼
ID Token + Access Token
 │
 ▼
Client Validates Tokens
 │
 ▼
Access Granted
```

---

## Skills Demonstrated

* Identity and Access Management (IAM)
* OpenID Connect (OIDC)
* OAuth 2.0 Authorization Code Flow
* Authentication Architecture
* Authorization Concepts
* Token-Based Authentication
* Claims Management
* Okta Administration
* Redirect URI Configuration
* Client Application Integration
* Identity Federation Concepts
* Modern Authentication Protocols

---

## Learning Outcomes

By completing this project, I gained hands-on experience implementing OpenID Connect authentication using Okta. The project demonstrates how modern applications authenticate users through an Authorization Server, securely exchange authorization codes for tokens, and consume claims to establish authenticated sessions. This lab reflects real-world authentication architectures used by cloud-native applications, SaaS platforms, and enterprise identity ecosystems.
**Flow:** Authorization Code Flow
**Project Type:** Authentication Protocol Lab
