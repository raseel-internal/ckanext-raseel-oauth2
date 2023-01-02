To install the plugin, **enter your virtualenv** and install the package using `pip` as follows:

```
pip install ckanext-oauth2
```

Add the following to your CKAN `.ini` (generally `/etc/ckan/default/production.ini`) file:

```
ckan.plugins = oauth2 <other-plugins>

## OAuth2 configuration

ckan.oauth2.register_url = https://YOUR_OAUTH_SERVICE/users/sign_up
ckan.oauth2.reset_url = https://YOUR_OAUTH_SERVICE/users/password/new
ckan.oauth2.edit_url = https://YOUR_OAUTH_SERVICE/settings
ckan.oauth2.authorization_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/auth
ckan.oauth2.token_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/token
ckan.oauth2.profile_api_url = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/userinfo
ckan.oauth2.client_id = opendata
ckan.oauth2.client_secret = Eht0N0PYqy8iDaq7WNEOKWJTWD9E5tzI
ckan.oauth2.scope = profile other.scope
ckan.oauth2.rememberer_name = auth_tkt
ckan.oauth2.profile_api_user_field = preferred_username
ckan.oauth2.profile_api_fullname_field = name
ckan.oauth2.profile_api_mail_field = email
ckan.oauth2.authorization_header = OAUTH2_HEADER
```

> **Note**: In case you are using FIWARE as OAuth2 provider, this is the concrete OAuth2 configuration you should use (e.g. using FIWARE Lab):
>
> ```
> ## OAuth2 configuration
> ckan.oauth2.register_url = https://account.lab.fiware.org/users/sign_up
> ckan.oauth2.reset_url = https://account.lab.fiware.org/users/password/new
> ckan.oauth2.edit_url = https://account.lab.fiware.org/idm/settings
> ckan.oauth2.authorization_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/auth
> ckan.oauth2.token_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/token
> ckan.oauth2.profile_api_url = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/userinfo
> ckan.oauth2.client_id = opendata
> ckan.oauth2.client_secret = YEht0N0PYqy8iDaq7WNEOKWJTWD9E5tzI
> ckan.oauth2.scope = all_info
> ckan.oauth2.profile_api_user_field = id
> ckan.oauth2.profile_api_fullname_field = preferred_username
> ckan.oauth2.profile_api_mail_field = email
> ckan.oauth2.authorization_header = Authorization
> ```
>
> And this is an example for using Google as OAuth2 provider:
>
> ```
> ## OAuth2 configuration
> ckan.oauth2.authorization_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/auth
> ckan.oauth2.token_endpoint = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/token
> ckan.oauth2.profile_api_url = https://dev-iam.raseel.city/realms/raseel/protocol/openid-connect/userinfo
> ckan.oauth2.client_id = opendata
> ckan.oauth2.client_secret = Eht0N0PYqy8iDaq7WNEOKWJTWD9E5tzI
> ckan.oauth2.scope = openid email profile
> ckan.oauth2.profile_api_user_field = preferred_username
> ckan.oauth2.profile_api_fullname_field = name
> ckan.oauth2.profile_api_mail_field = email
> ckan.oauth2.authorization_header = Authorization
> ```

You can also use environment variables to configure this plugin, the name of the environment variables are:

- `CKAN_OAUTH2_REGISTER_URL`
- `CKAN_OAUTH2_RESET_URL`
- `CKAN_OAUTH2_EDIT_URL`
- `CKAN_OAUTH2_AUTHORIZATION_ENDPOINT`
- `CKAN_OAUTH2_TOKEN_ENDPOINT`
- `CKAN_OAUTH2_PROFILE_API_URL`
- `CKAN_OAUTH2_CLIENT_ID`
- `CKAN_OAUTH2_CLIENT_SECRET`
- `CKAN_OAUTH2_SCOPE`
- `CKAN_OAUTH2_REMEMBERER_NAME`
- `CKAN_OAUTH2_PROFILE_API_USER_FIELD`
- `CKAN_OAUTH2_PROFILE_API_FULLNAME_FIELD`
- `CKAN_OAUTH2_PROFILE_API_MAIL_FIELD`
- `CKAN_OAUTH2_AUTHORIZATION_HEADER`

**Additional notes**:

- This extension only works when your CKAN instance is working over HTTPS, since OAuth 2.0 depends on it. You can follow the [Starting CKAN over HTTPs tutorial](https://github.com/conwetlab/ckanext-oauth2/wiki/Starting-CKAN-over-HTTPs) to learn how to do that.
- You can run the extension to connect to a OAuth2 server using HTTP, or to a server using an invalid certificate (e.g. a self-signed one), by editing the file `/etc/apache2/envvars` and adding the following environment variable, or directly exporting the variable in the shell if you are executing development server with "paster serve ..." :

```
export OAUTHLIB_INSECURE_TRANSPORT=True
```

- The callback URL that you should set on your OAuth 2.0 is: `https://YOUR_CKAN_INSTANCE/oauth2/callback`, replacing `YOUR_CKAN_INSTANCE` by the machine and port where your CKAN instance is running.
- If you are connecting to FIWARE KeyRock v6 or v5, you have to set `ckan.oauth2.legacy_idm` to `true`.

Refer to this document for integration between CKAN and WSO2-IS IDM using oauth2 with settings:
https://github.com/conwetlab/ckanext-oauth2/wiki/Integration-between-WSO2-IS-and-CKAN-using-Oauth2
