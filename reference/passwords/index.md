---
title: Passwords API Reference
has_superbar: Yes
route_path: /wpas-api/v1/users/<user_id>/passwords
resource: Password
---

<section class="route">
	<div class="primary">
		{% include reference-parts/schema.html schema=site.data.password.schema %}
	</div>
	<div class="secondary">
		<h3>Example Request</h3>
		
		<code>$ curl -X OPTIONS -i http://demo.getawesomesupport.com/wp-json{{ site.data.password.routes[page.route_path].nicename}}</code>
	</div>
</section>

{% assign route=site.data.password.routes['/wpas-api/v1/users/<user_id>/passwords'] %}
{% include reference-parts/list-item.html route=route %}

{% assign route=site.data.password.routes['/wpas-api/v1/users/<user_id>/passwords'] %}
{% include reference-parts/create-item.html route=route %}

{% assign route=site.data.password.routes['/wpas-api/v1/users/<user_id>/passwords/<slug>'] %}
{% include reference-parts/delete-item.html route=route index=0 %}
