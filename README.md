This is a docker recipe and accompanying scripts for an Nginx reverse proxy server solution with built-in oauth2 capabilities via oauth-proxy. It has the following capabilities/project goals:

1)Automatic deployment and renewel of LetsEncrypt certificate via a Google api service account.

2)Bundled Oauth2-proxy capabilities against a Google authentication oauth2 set of credentials. Backed by Redis for stability.

Each sitelist and hostlist are arrays that the startup scripts will loop through, and in order for Nginx to start correctly you must have Docker containers present on the same docker network as nginx_frontdoor is configure on, or it will fail to start.

The recipe heavily utilizes docker-compose .env file for variable substitution. The following settings are implicated:

#For the purposes of sites and hosts, sites are the front-end web site full DNS names, and the host list is the corresponding docker hosts name that its assigned to at the same order point in the list. Each site and host is seperated by a single space.
Sites & hosts protected via Oauth. A sample .env file is as follows:
```
#Sites and hosts protected by Oauth:
oauth_sitelist=site1.mysite.com site2.mysite.com
oauth_hostlist=site1 site2

#Sites and hosts not protected by Oauth:
unoauth_sitelist=protected1.mysite.com protected2.mysite.com
unoauth_hostlist=protected1:8000 protected2:4211
#The network name to use for the docker containers:
network_name=docker_bridge1
#This is used in naming a lot of stuff.
proj_name=frontdoor

#The credentials for updating DNS records
client_id=
client_secret=
cookie_secret=
#Domains which are protected by oauth2
cookie_domains=l.taxsaverplan.com
#Listing of users allows to connect to resources protected by oauth2-proxy, the full email address is required, and each user is simply separated by a space:
oauth_users=user1@mysite.com user2@mysite.com

#google.json settings for oauth-proxy, these can be found under the credentials tab and downloaded from Google as a google.json file:
google_json_project_id=
google_json_private_key_id=
google_json_private_key=
google_json_client_email=
google_json_client_id=
google_json_auth_uri=
google_json_token_uri=
google_json_auth_provider_x509_cert_url=
google_json_client_x509_cert_url=
```

For each site that you specify in oauth_sitelist, or unoauth_sitelist a template will be used to generate it under frontdoor_nginx/templates. You can override this placing the Nginx configuration file in /sites. The startup script auto deploys any LetsEncrypt certificates that are not already present for any site with a sitefile in /sites, regardless of whether its in the site list or not. With Redis, oauth2-proxy should be solid and never ask you to login after the first time, if it starts bugging out you can fix it by completely resetting your browser.




