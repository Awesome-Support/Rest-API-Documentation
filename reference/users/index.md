---
title: Users API Reference
has_superbar: Yes
route_path: /wpas-api/v1/users
resource: User
---

<section class="route">
	<div class="primary">
		{% include reference-parts/schema.html schema=site.data.user.schema %}
	</div>
	<div class="secondary">
		<h3>Example Request</h3>

		<code>$ curl -X OPTIONS -i http://demo.wp-api.org/wp-json{{ site.data.user.routes['/wpas-api/v1/users'].nicename }}</code>
	</div>
</section>

{% assign route=site.data.user.routes['/wpas-api/v1/users'] %}
{% include reference-parts/list-item.html route=route %}

{% assign route=site.data.user.routes['/wpas-api/v1/users/<id>'] %}
{% include reference-parts/get-item.html route=route %}

{% assign route=site.data.user.routes['/wpas-api/v1/users'] %}
{% include reference-parts/create-item.html route=route %}

{% assign route=site.data.user.routes['/wpas-api/v1/users/<id>'] %}
{% include reference-parts/update-item.html route=route %}

{% assign route=site.data.user.routes['/wpas-api/v1/users/<id>'] %}
{% include reference-parts/delete-item.html route=route %}