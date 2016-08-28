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

or specify `all-but` and then list hosts that should NOT be
protected by basic authentication:

`AUTH-REQUIRED: all-but`
`AUTH-NOTREQUIRED: no-auth.hostname.tld`

Then mount container file `/etc/nginx/htpasswd` to your host,
and populate it with htpasswd utility.

### Directory listing

To enable nginx's directory listing, specify the virtual hosts
you want to allow listing directory contents:

`AUTOINDEX: allow-listing.hostname.tld`

## Known issues

Nginx does not send HSTS header with pages that require authentication
but have not yet been authenticated (ie. with HTTP response 401). This
results to a situation where HSTS seems not to be enabled on auth required
pages when authentication is not yet completed by client.

See more info at http://serverfault.com/questions/628448/nginx-hsts-on-a-page-with-www-authentication

I am currently investigating workaround for this.
