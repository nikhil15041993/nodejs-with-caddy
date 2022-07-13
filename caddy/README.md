 Caddy is a powerful platform to serve your web applications and services. 

## Reverse Proxy a Node.js App Using a Caddyfile

After installing Caddy you can find a caddy directory in /etc/caddy. This directory contains a default Caddyfile. You can change this existing Caddyfile to configure the reverse proxy.

Here’s a basic reverse proxy setup reverse proxying all HTTP requests to a locally running server on port 3000. We’re assuming you started your Node.js server on port 3000 already.

Now, open /etc/caddy/Caddyfile (for example with nano) and adjust the contents to this:
```
:80 {
  reverse_proxy localhost:3000
}
```
Save the changes and tell Caddy to serve the configuration by running the following command from the /etc/caddy directory:
```
caddy run Caddyfile  
```

## Reverse Proxying a Domain

## Create a New Caddyfile
We use a dedicated Caddyfile to serve the Supercharge website. The website’s Caddyfile is named superchargejs.com. It lives beside the default Caddyfile.

The content of the superchargejs.com Caddyfile is this:
```
superchargejs.com {  
  reverse_proxy localhost:2021
}
```
We then import the Caddyfile for superchargejs.com inside of the default Caddyfile. Open and edit /etc/caddy/Caddyfile to import the configuration for the Supercharge website:

import ./superchargejs.com
```
:80 {
  reverse_proxy localhost:3000
}
```

Then reload Caddy to pick up the changed configuration:
```
$ caddy reload Caddyfile
```

## At a subpath
Here is the equivalent of the sample config above but running under a sub path.

superchargejs.com {
  route /gotify/* {
    uri strip_prefix /gotify
    # Set the port to the one you are using in gotify
    reverse_proxy localhost:1245
  }
  redir /gotify /gotify/
}
