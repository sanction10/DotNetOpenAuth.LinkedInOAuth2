DotNetOpenAuth OAuth2 Client for LinkedIn
======================================

This is an OAuth2 client to use with the DotNetOpenAuth project. The following code is an adaptation of [Matt Johnson's](https://github.com/mj1856) [DotNetOpenAuth.GoogleOAuth2](https://github.com/mj1856/DotNetOpenAuth.GoogleOAuth2) project

## Setup

 1. Setup your LinkedIn App using the [LinkedIn Developer Network](https://www.linkedin.com/secure/developer).    

 2. Compile from source and reference. (NuGet coming soon)

 3. Register the client instead of the existing LinkedIn OpenId client.

        var client = new LinkedInOAuth2Client("yourClientId", "yourClientSecret");
        OAuthWebSecurity.RegisterClient(client);

## Usage

Just like any other `OAuthWebSecurity` client, except you need one extra hook:

        // add this line
        LinkedInOAuth2Client.RewriteRequest();

        // it belongs right before your existing call to
        OAuthWebSecurity.VerifyAuthentication(....)

This is needed because LinkedIn requires that any extra querystring parameters for the
redirect be packed into a single parameter called `state`.  Since `OAuthWebSecurity` needs
two parameters, `__provider__` and `__sid__` - we have to rewrite the url.


## Disclaimer

I don't work for Google, Microsoft, or DNOA.  This is released under the [MIT](LICENCE.txt) licence.  Do what you want with it.
