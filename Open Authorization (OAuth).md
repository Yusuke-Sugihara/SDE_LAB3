# SDE Lab 03: REST ADVANCED
## DOCUMENTATION: Open Authorization (OAuth) 

### Open Authorization (OAuth)
Open Authorization, commonly known as OAuth, is an open standard protocol that allows secure third-party access to resources without sharing the user's credentials (e.g., username and password). OAuth is widely used for granting access to web services, APIs, and other online resources while keeping the user's data and credentials safe. Here are more details about how OAuth works:



![Tokenization in APIs](https://github.com/Yusuke-Sugihara/SDE_LAB3/blob/main/Images/Image_Tokenization.jpg)

### Key Concepts in OAuth:
## Roles:

- **Resource Owner**: This is the user who owns the resources, such as their data or accounts on a service.
- **Client**: The application or service that wants to access the user's resources on their behalf.
- **Authorization Server**: Responsible for authenticating the user and issuing access tokens after the user grants permission.
- **Resource Server**: Hosts the protected resources and enforces access controls. It verifies the access token to ensure that the client has the necessary permissions.

## Access Tokens:

Access tokens are temporary credentials that are issued by the authorization server and presented by the client to access the user's resources on the resource server. They typically have a limited lifespan and scope, making them more secure than long-lived credentials.

## OAuth Flow:

The OAuth protocol defines several authorization flows to facilitate different use cases, but the most common one is the OAuth 2.0 authorization code flow. Here's how it works:

1. **Authorization Request**: The client (third-party application) redirects the user to the authorization server. The client includes information about the requested scope and the redirection URI.

2. **User's Approval**: The user is prompted to log in and grant the client access to their resources. The user's consent is crucial to maintain control over their data.

3. **Authorization Grant**: If the user grants permission, the authorization server issues an authorization code to the client's specified redirection URI.

4. **Access Token Request**: The client exchanges the authorization code for an access token by sending a request to the authorization server.

5. **Access Token Issuance**: The authorization server validates the client and the authorization code, then issues an access token and optionally a refresh token.

6. **Accessing Resources**: The client uses the access token to make requests to the resource server, which verifies the token to determine if the client has the necessary permissions.

## OAuth Scopes:

Scopes are used to define the specific permissions and access levels requested by the client. For example, a client may request read-only access to a user's profile or full access to their account. Scopes allow fine-grained control over what the client can do with the user's resources.

OAuth 2.0 also introduced the concept of bearer tokens, which are self-contained tokens used by the client to authenticate and access resources. The client presents the token, and the resource server validates it.

OAuth is widely used for Single Sign-On (SSO) scenarios, social media logins, and API access management in a secure and user-friendly manner. It has become a fundamental part of modern web and mobile application development, allowing users to grant controlled access to their data and resources while maintaining their privacy and security.
