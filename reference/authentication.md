---
page: authentication
title: Authentication
layout: reference
---

<section class="route">
<div class="primary" markdown="1">
<h1>{{ page.title }}</h1>

There are several options for authenticating with the API. The basic choice boils
down to:

* Are you a plugin/theme running on the site? Use **cookie authentication**
* Are you a desktop/web/mobile client accessing the site externally? Use **basic authentication**.
</div>
</section>

<section class="route">
<div class="primary" markdown="1">

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

</div>

<div class="secondary" markdown="1">
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

</div>
</section>

<section class="route">
<div class="primary" markdown="1">

Basic Authentication
--------------------
[HTTP Basic Authentication][http-basic] (published as RFC2617) can be used to authenticate external services. It can use either the user's username and password or the username and API password (located in the user's edit screen).

API passwords are the more secure method of authentication since they are unique, random, and easily revokable. Additionally, API passwords are valid only for the REST API and may not be used to log in to WordPress. Only use the user's password for authentication when the user will also be logging into the website.

To use Basic authentication, simply pass the username and password with each
request through the `Authorization` header. This value should be encoded (using
base64 encoding) as per the HTTP Basic specification.

</div>

<div class="secondary" markdown="1">

This is an example of how to update a post, using these authentications, via the
WordPress HTTP API:

```php
$headers = array (
	'Authorization' => 'Basic ' . base64_encode( 'admin' . ':' . '0qND QR5t tX4y qa0S eb4c tjrq' ),
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
</div>
</section>
