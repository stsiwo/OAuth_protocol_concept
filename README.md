# OAuth and OpenID Connect 

## Q&A

### always get 'redirect_uri_mismatch' even if properly setting the same url

make sure setting the same uri at the following: 

1. Google API Console
2. FrontEnd (e.g., [react-google-login libarary](https://github.com/anthonyjgrove/react-google-login))

```
<GoogleLogin
        clientId="380002512591-e0puk82lvvcblkao2am46ui2d7sedk6m.apps.googleusercontent.com"
        buttonText="Sign In With Google"
        onSuccess={handleSuccess}
        onFailure={handleFailure}
        cookiePolicy={"single_host_origin"}
        responseType="code" // authorization code (not access token directly)
        redirectUri="http://localdev.com:3000" // <- must match
        uxMode="redirect"
      />

```

3. BackEnd (e.g., [Go OAuth2 package](https://pkg.go.dev/golang.org/x/oauth2))

```
      ClientID:     env.GetEnv().OAuth.Google.ClientID,
			ClientSecret: env.GetEnv().OAuth.Google.ClientSecret,
			Endpoint:     google.Endpoint,
			RedirectURL:  "http://localdev.com:3000", // <- must match
```

Also, **it might take a little time that Google API Console sets up the url so you need to wait a little bit**.

Also, make sure you refresh the page with cache clear and hard.

refs:
[take some time after change the url at Google API Console](https://stackoverflow.com/questions/11485271/google-oauth-2-authorization-error-redirect-uri-mismatch)
