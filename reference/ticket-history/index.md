---
title: Ticket History API Reference
has_superbar: Yes
route_path: /wpas-api/v1/tickets/<ticket_id>/history
resource: Ticket History
---

<section class="route">
	<div class="primary">
		{% include reference-parts/schema.html schema=site.data.ticket_history.schema %}
	</div>
	<div class="secondary">
		<h3>Example Request</h3>

		<code>$ curl -X OPTIONS -i http://demo.getawesomesupport.com/wp-json{{ site.data.ticket_history.routes[page.route_path].nicename }}</code>
	</div>
</section>

{% assign route=site.data.ticket_history.routes['/wpas-api/v1/tickets/<ticket_id>/history'] %}
{% include reference-parts/list-item.html route=route %}

{% assign route=site.data.ticket_history.routes['/wpas-api/v1/tickets/<ticket_id>/history/<id>'] %}
{% include reference-parts/get-item.html route=route %}
