Getty Images Connect API
========================
Our set of APIs enable seamless integration of Getty Images' expansive content, powerful search 
and rich metadata directly into your internal workflows, products and services. With Connect's API 
solutions, you can fully control, customize and scale as you grow.

The Connect API uses JSON over HTTP POST to allow you to build applications capable of search and 
download on Getty Images using an active download agreement.

##Checklist
* Activate a download agreement for organization.
* Get credentials for your application.
* Familiarize yourself with the core concepts and the API operations.
* Begin developing your application.

##Endpoints

###Session Operations
- **[<code>POST</code> CreateSession](https://github.com/gettyimages/connect/documentation/endpoints/session/CreateSession.md)**
- **[<code>POST</code> RenewSession](https://github.com/gettyimages/connect/documentation/endpoints/session/RenewSession.md)**

###Search Operations
- **[<code>POST</code> SearchForImages](https://github.com/gettyimages/connect/documentation/endpoints/search/SearchForImages.md)**
- **[<code>POST</code> GetImageDetails](https://github.com/gettyimages/connect/documentation/endpoints/search/GetImageDetails.md)**
- **[<code>POST</code> GetEventDetails](https://github.com/gettyimages/connect/documentation/endpoints/search/GetEventDetails.md)**
- **[<code>POST</code> SearchForVideos](https://github.com/gettyimages/connect/documentation/endpoints/search/SearchForVideos.md)**

###Download Operations
- **[<code>POST</code> GetImageDownloadAuthorizations](https://github.com/gettyimages/connect/documentation/endpoints/download/GetImageDownloadAuthorizations.md)**
- **[<code>POST</code> GetLargestImageDownloadAuthorizations](https://github.com/gettyimages/connect/documentation/endpoints/download/GetLargestImageDownloadAuthorizations.md)**
- **[<code>POST</code> CreateDownloadRequest](https://github.com/gettyimages/connect/documentation/endpoints/download/CreateDownloadRequest.md)**

##Core Concepts

###Authentication
All operations in the Getty Images Connect API require an authentication token 
argument provided in the RequestHeader. An authentication token securely 
identifies the caller of an operation. When called, an operation checks the validity of 
the provided authentication token before executing the request. A malformed, 
invalid, or expired token causes an operation to fail.

Clients get authentication tokens by authenticating themselves using the 
CreateSession operation. Clients are required to provide the participant system's 
credentials and a specific user's credentials. Authenticating using only system 
credentials results in anonymous tokens. Providing user credentials results in a fully 
authenticated token. Fully authenticated tokens are generally required by all 
operations in the Getty Images Connect API.

###Secure-Only Operations
Some operations are secure only. These operation must be called over an SSL 
connection with a secure token. They include CreateSession, RenewSession, and 
CreateDownloadRequest.

The required combination of passing a secure token over SSL prevents a "man-in-the-middle" 
exploitation where an attacker sniffs tokens from a non-SSL connection, then uses the token 
to impersonate the client, thereby possibly gaining access to sensitive information or 
processes. Operations that could expose sensitive data only accept secure tokens 
over SSL. As long as these tokens are always and only passed over SSL, attackers can 
never acquire a secure token with which to impersonate a valid customer.

Secure authentication tokens are provided by CreateSession operation. Secure 
tokens are essentially the same as standard tokens, with the difference that secure 
tokens can only be used over SSL connections. Calling any operation with a secure 
token over a non-SSL connection will result in an error.

###Token Expiration and Renewal
Tokens expire after 30 minutes. Clients can renew a token before it expires by using 
the RenewSession operation, without having to provide credentials again. We 
recommend clients track each token's time-to-expiration, and pro-actively call  
RenewSession prior to the token's expiration.

