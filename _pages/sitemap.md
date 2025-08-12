---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

A list of all the posts and pages found on the site. 

<h2>Pages</h2>
{% for post in site.pages %}
  {% include archive-single-list.html %}
{% endfor %}

[XML version]({{ base_path }}/sitemap.xml)