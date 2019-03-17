---
title: Domain Registrars
layout: default
---

{% if site.tlds.size == 1 %}
# {{ site.tlds[0] | upcase }} domain registrars
{% else %}
# {{ page.title }}
{% endif %}

{% if site.tlds.size > 1 %}
Initial content for all domain registrars:

<ul>
{% for tld in site.tlds %}
	<li>{{ tld }}</li>
{% endfor %}
</ul>

{% endif %}

{% for tld in site.tlds %}
{% assign data = site.data[tld] %}
{% if site.tlds.size > 1 %}
<h2 id="{{ tld }}">{{ tld | upcase }} registrars</h2>
{% endif %}

<i class="{{ tld }} flag"></i>
Central registry: <a href="{{ data.registry.url }}">{{ data.registry.name }}</a>

<table class="ui sortable structured celled table">
	<thead>
		<tr>
			<th>Name</th>
			<th class="center aligned">DNSSEC</th>
			<th class="center aligned">IPv6</th>
			<th class="center aligned">API</th>
			<th class="center aligned">Docs</th>
			<th class="center aligned">Format</th>
			<th class="center aligned">SDK languages</th>
			<th class="center aligned">Renewal</th>
		</tr>
	</thead>
	<tbody>
	{% for registrar in data.registrars %}
	<tr>
		<td><a href="{{ registrar.url }}">{{ registrar.name }}</a></td>
		<td class="center aligned">{% if registrar.dnssec %}<i class="large green checkmark icon">y</i>{% endif %}</td>
		<td class="center aligned">{% if registrar.ipv6 %}<i class="large green checkmark icon">y</i>{% endif %}</td>
		<td class="center aligned">{% if registrar.api %}<i class="large green checkmark icon">y</i>{% endif %}</td>
		<td class="center aligned">{% if registrar.api.docs_url %}<a href="{{ registrar.api.docs_url }}"><i class="large file alternate outline icon">y</i></a>{% endif %}</td>
		<td class="center aligned">{% if registrar.api.formats %}{{ registrar.api.formats | join: ", " }}{% endif %}</td>
		<td class="center aligned">{% if registrar.api.formats %}{{ registrar.api.sdk_languages | join: ", " }}{% endif %}</td>
		<td>{% if registrar.price.renewal %}{{ registrar.price.renewal | money: "CZK" }}{% endif %}</td>
	</tr>
	{% endfor %}
	</tbody>
</table>
{% endfor %}
