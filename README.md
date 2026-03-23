# Openshift-Grafana-EntraID-Auth

Goto Microsoft Azure and create app registration

create client secret. 

goto Grafana  -- admin -- authentication and select entra ID 

update the entra ID by using client secret for authentication 

add the client ID , auth url and token url. 

use this as signout redirect url :    

```
https://login.microsoftonline.com/27610e39-e1af-42c6-b20f-80ca8c8579c6/oauth2/v2.0/logout?post_logout_redirect_uri=https%3A%2F%2Fgrafana-default.apps.bny-c-ec-npr-01.nlng.net%2Flogin
```

edit Grafana object and edit this block 

oc edit grafana grafana-a -n default

```
spec:
  config:
    auth:
      disable_login_form: "false"
    auth.azuread:
      enabled: "true"
      signout_redirect_url: https://login.microsoftonline.com/<TENANT-ID>/oauth2/v2.0/logout?post_logout_redirect_uri=https%3A%2F%2Fgrafana-default.apps.bny-c-ec-npr-01.nlng.net%2Flogin
    log:
      mode: console
    security:
      admin_password: start
      admin_user: root
    server:
      root_url: https://grafana-default.apps.bny-c-ec-npr-01.nlng.net
```



Also add this URI in Entra App Registration → Authentication → redirect URI :

```
https://grafana-default.apps.bny-c-ec-npr-01.nlng.net/login
https://grafana-default.apps.bny-c-ec-npr-01.nlng.net/login/azuread
```
