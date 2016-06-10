# HTTPS-PORTAL

This is a fork of [https://hub.docker.com/r/steveltn/https-portal/](https://hub.docker.com/r/steveltn/https-portal/)
which includes the following extra features:

- HSTS support if specified in environment variables
- HTTP basic authentication per virtual host if specified

See [https://hub.docker.com/r/steveltn/https-portal/](https://hub.docker.com/r/steveltn/https-portal/)
for documentation on how to use this Docker image.

## New features

To use these features, set the following environment variables
in either Docker run command, or in docker-compose file.

### HSTS

Enable HSTS support for all virtual hosts

`HSTS=true`

### HSTS in all subdomains

Specify that all subdomains should use HTTPS, regardless where
they are hosted. Be carefull you don't break your domain with this.

`HSTS-SUBDOMAINS=true`

### HTTP basic auth

Specify the virtual hosts you want to require authentication

`AUTH-REQUIRED: first.hostname.tld, second.hostname.tld`

or just specify `all` to require authentication on all
virtualhosts https-portal is serving.

`AUTH-REQUIRED: all`

Then mount container file `/etc/nginx/htpasswd` to your host,
and populate it with htpasswd utility.
