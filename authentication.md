---
title: Authentication
---

There are several options for authenticating with the API. The basic choice boils
down to:

* Are you a plugin/theme running on the site? Use **cookie authentication**
* Are you a desktop/web/mobile client accessing the site externally? Use **basic authentication**.


Cookie Authentication
---------------------
Cookie authentication is the basic authentication method included with
WordPress. When you log in to your dashboard, this sets up the cookies correctly
for you, so plugin and theme developers need only to have a logged-in user.

However, the REST API includes a technique called [nonces][] to avoid [CSRF][] issues.
This prevents other sites from forcing you to perform actions without explicitly
intending to do so. This requires slightly special handling for the API.

For developers using the built-in Javascript API, this is handled automatically
for you. This is the recommended way to use the API for plugins and themes.
Custom data models can extend `wp.api.models.Base` to ensure this is sent
correctly for any custom requests.

For developers making manual Ajax requests, the nonce will need to be passed
with each request. The API uses nonces with the action set to `wp_rest`. These
can then be passed to the API via the `_wpnonce` data parameter (either POST
data or in the query for GET requests), or via the `X-WP-Nonce` header.

It is important to keep in mind that this authentication method relies on WordPress
cookies. As a result this method is only applicable when the REST API is used inside
of WordPress and the current user is logged in. In addition, the current user must
have the appropriate capability to perform the action being performed.

As an example, this is how the built-in Javascript client creates the nonce:

```php
<?php
wp_localize_script( 'wp-api', 'wpApiSettings', array( 'root' => esc_url_raw( rest_url() ), 'nonce' => wp_create_nonce( 'wp_rest' ) ) );
```

This is then used in the base model:

```javascript
options.beforeSend = function(xhr) {
	xhr.setRequestHeader('X-WP-Nonce', wpApiSettings.nonce);

	if (beforeSend) {
		return beforeSend.apply(this, arguments);
	}
};
```

Here is an example of editing the title of a post, using jQuery AJAX:

```javascript
$.ajax( {
    url: wpApiSettings.root + 'wpas-api/v1/tickets/1',
    method: 'POST',
    beforeSend: function ( xhr ) {
        xhr.setRequestHeader( 'X-WP-Nonce', wpApiSettings.nonce );
    },
    data:{
        'title' : 'New Ticket Title'
    }
} ).done( function ( response ) {
    console.log( response );
} );
```

[nonces]: http://codex.wordpress.org/WordPress_Nonces
[CSRF]: http://en.wikipedia.org/wiki/Cross-site_request_forgery

Application Passwords and Basic Authentication
---------------------------------------------
Basic authentication is an optional authentication handler for external clients.
Due to the complexity of OAuth authentication, basic authentication can be
useful during development. However, Basic authentication requires passing your
username and password on every request, as well as giving your credentials to
clients, so it is heavily discouraged for production use.

Application passwords are used similarly, however instead of providing your normal
account password, unique and easily revokable passwords are generated from your
edit profile screen in the WordPress admin.  These application passwords are valid
exclusively for the REST API and the legacy XML-RPC API and may not be used to log
in to WordPress.

Both basic authentication and application passwords use [HTTP Basic Authentication][http-basic]
(published as RFC2617) and are supported by the Awesome Support API.

To use Basic authentication, simply pass the username and password with each
request through the `Authorization` header. This value should be encoded (using
base64 encoding) as per the HTTP Basic specification.

This is an example of how to update a post, using these authentications, via the
WordPress HTTP API:

```php
$headers = array (
	'Authorization' => 'Basic ' . base64_encode( 'admin' . ':' . '12345' ),
);
$url = rest_url( 'wpas-api/v1/tickets/1' );

$data = array(
	'title' => 'Support Ticket Title' 
);

$response = wp_remote_post( $url, array (
    'method'  => 'POST',
    'headers' => $headers,
    'body'    =>  $data
) );
```
    

[http-basic]: https://tools.ietf.org/html/rfc2617
[basic-auth-plugin]: https://github.com/WP-API/Basic-Auth
[application-passwords]: https://github.com/georgestephanis/application-passwords
