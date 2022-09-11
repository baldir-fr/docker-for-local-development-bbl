
## Introduction

- 🔒[Authorisation Grant](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-1.3)
  - 🎟 [Authorization Code](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-1.3.1)
  - 🍹  [Refresh Token](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-1.3.2)
- 🎁 [Access Token](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-1.4)

## Client Registration

- 🛂 [Client registration](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-2)
  - Confidential client
    - Backend API
  - Public client
    - Browser-based application
- 🆔 [Client Identifier](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-2.2)
  - `client_id`
- ↩️ [Client Redirection Endpoint](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-2.3) / [Registration Requirements](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-2.3.1)
  - `https://my-browser-app/auth/callback`
  - absolute URI
  - exact match URI(s)
- [Preventing CSRF Attacks](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-2.3.3)
  - Validate OIDC `nonce` parameter

## Protocol Endpoints

- [Protocol Endpoints](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3)
  - 🏢🔒 [Authorization Endpoint](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3.1)
      - **👤 Resource owner** interacts with **🏢 Authorization Endpoint** to obtain **🔒 Authorization Grant** 
      - [OIDC Authorization Endpoint](https://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint)
    - Authorization Request
  - 🏢🎟 [Token Endpoint](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3.2)
    - HTTP `POST` method
    - 🎟❓[Token Request](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3.2.2)
      - \* `client_id`
      - \* `grant_type` : **"authorization_code"** | **"refresh_token"** | "client_credentials"
      - `scope`
    - 🎟✅🍹 [Token Response](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3.2.3)
      - \* `access_token` : 🎟 Access Token
      - \* `token_type`: "Bearer" |  ([Access Token types](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-5.1))
      - `expires_in`
      - `scope`
      - `refresh_token` : 🍹 Refresh Token (optional)
      - Example : 
        ```json 
        {
           "access_token":"2YotnFZFEjr1zCsicMWpAA",
           "token_type":"Bearer",
           "expires_in":3600,
           "refresh_token":"tGzv3JOkF0XG5Qx2TlKWIA"
        }
        ```
    - ❌ [Error Response](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-3.2.3.1)
      - HTTP status `400`
      - \* `error` : "invalid_request" | "invalid_client" (usually HTTP status `401`) | "invalid_grant" | "unauthorized_client" | "unsupported_grant_type" | "invalid_scope"
      - `error_description`
      - `error_uri`
      - Example:
        ```json
        {
           "error":"invalid_request"
        }
        ```
        
## Grant Types

- [Grant Types](
https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-4)
  - [Authorization Code Grant](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-4.1)
    - [Authorization Request](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-4.1.1)
      - \* `response_type` : "code"
        - OIDC extension response types
      - \* `client_id`
      - `code_challenge`
      - `code_challenge_method`
      - `redirect_uri`
      - `scope`
      - `state`
      - Example
        ```
        GET /authorize
         ?response_type=code
         &client_id=s6BhdRkqt3
         &state=xyz
         &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
         &code_challenge=6fdkQaPm51l13DSukcAH3Mdx7_ntecHYd1vi3n0hMZY
         &code_challenge_method=S256
         HTTP/1.1
         Host: server.example.com
        ```
    - [Authorization Response](https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1-05#section-4.1.2)
      - 

## Accessign Protected Resources

