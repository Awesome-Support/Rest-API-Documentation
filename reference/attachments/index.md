---
title: Attachments API Reference
has_superbar: Yes
route_path: /wpas-api/v1/attachments
resource: Attachment
---

<section class="route">
	<div class="primary">
		{% include reference-parts/schema.html schema=site.data.attachment.schema %}
	</div>
	<div class="secondary">
		<h3>Example Request</h3>

		<code>$ curl -X OPTIONS -i http://demo.getawesomesupport.com/wp-json{{ site.data.attachment.routes[page.route_path].nicename }}</code>
	</div>
</section>

{% assign route=site.data.attachment.routes['/wpas-api/v1/attachments'] %}
{% include reference-parts/list-item.html route=route %}

{% assign route=site.data.attachment.routes['/wpas-api/v1/attachments/<id>'] %}
{% include reference-parts/get-item.html route=route %}

{% assign route=site.data.attachment.routes['/wpas-api/v1/attachments'] %}
{% include reference-parts/create-item.html route=route %}

{% assign route=site.data.attachment.routes['/wpas-api/v1/attachments/<id>'] %}
{% include reference-parts/update-item.html route=route %}

{% assign route=site.data.attachment.routes['/wpas-api/v1/attachments/<id>'] %}
{% include reference-parts/delete-item.html route=route %}
