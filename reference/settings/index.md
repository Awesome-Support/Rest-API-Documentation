---
title: Settings API Reference
has_superbar: Yes
route_path: /wpas-api/v1/settings
resource: Setting
---

<section class="route">
	<div class="primary">
		{% include reference-parts/schema.html schema=site.data.settings.schema %}
	</div>
	<div class="secondary">
		<h3>Example Request</h3>

		<code>$ curl -X OPTIONS -i http://demo.getawesomesupport.com/wp-json{{ site.data.settings.routes['/wpas-api/v1/settings'].nicename }}</code>
	</div>
</section>

{% assign route=site.data.settings.routes['/wpas-api/v1/settings'] %}
{% include reference-parts/update-settings.html route=route %}
