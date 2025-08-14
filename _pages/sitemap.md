---
layout: page
title: "Sitemap"
permalink: /sitemap/
author_profile: true
sitemap: false
search_exclude: true
robots: noindex,follow
---

{% include base_path %}

A human-friendly overview of the site. Updated {{ site.time | date: "%Y-%m-%d" }}.

<style>
.sitemap-section { margin: 1.25rem 0 2rem; }
.sitemap-section h2 { margin-bottom: .35rem; }
.sitemap-muted { opacity: .7; font-size: .95em; }
.sitemap-list { margin: .25rem 0 0 1rem; }
.sitemap-list li { margin: .2rem 0; }
.sitemap-year { margin-top: .5rem; font-weight: 600; }
</style>

{%- assign utility_slugs = "404.html|^/categories/|^/tags/|^/page-archive/|^/collection-archive/|^/year-archive/|^/sitemap/|^/markdown/|^/markdown_generator/|^/non-menu-page/|^/terms/|^/talkmap.html" -%}

<div class="sitemap-section" id="pages">
  <h2>Pages</h2>
  <ul class="sitemap-list">
  {%- assign clean_pages = site.pages
      | where_exp: "p","p.sitemap != false"
      | where_exp: "p","p.title"
      | where_exp: "p","p.url"
  -%}
  {%- for p in clean_pages -%}
    {%- assign is_util = p.url =~ utility_slugs -%}
    {%- if is_util %}{% continue %}{% endif -%}
    {%- if p.url == "/" %}{% continue %}{% endif -%} {# Home is obvious #}
    <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
  {%- endfor -%}
  </ul>
</div>

{%- if site.posts and site.posts != empty -%}
<div class="sitemap-section" id="posts">
  <h2>News & Updates</h2>
  {%- assign posts = site.posts | where_exp: "p","p.sitemap != false" -%}
  {%- assign years = posts | map: "date" | map: "year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for post in posts -%}
        {%- if post.date | date: "%Y" == y -%}
          <li>
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            <span class="sitemap-muted">— {{ post.date | date: "%b %d" }}</span>
          </li>
        {%- endif -%}
      {%- endfor -%}
    </ul>
  {%- endfor -%}
</div>
{%- endif -%}

{%- if site.publications and site.publications != empty -%}
<div class="sitemap-section" id="publications">
  <h2>Publications</h2>
  {%- assign pubs = site.publications | where_exp: "p","p.sitemap != false" -%}
  {%- assign years = pubs | map: "date" | map: "year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for p in pubs -%}
        {%- if p.date and p.date | date: "%Y" == y -%}
          <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
        {%- endif -%}
      {%- endfor -%}
    </ul>
  {%- endfor -%}
</div>
{%- endif -%}

{%- if site.talks and site.talks != empty -%}
<div class="sitemap-section" id="talks">
  <h2>Talks</h2>
  {%- assign talks = site.talks | where_exp: "t","t.sitemap != false" -%}
  {%- assign years = talks | map: "date" | map: "year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for t in talks -%}
        {%- if t.date and t.date | date: "%Y" == y -%}
          <li>
            <a href="{{ t.url | relative_url }}">{{ t.title }}</a>
            {%- if t.venue %} <span class="sitemap-muted">— {{ t.venue }}</span>{% endif -%}
          </li>
        {%- endif -%}
      {%- endfor -%}
    </ul>
  {%- endfor -%}
</div>
{%- endif -%}

{%- if site.teaching and site.teaching != empty -%}
<div class="sitemap-section" id="teaching">
  <h2>Teaching</h2>
  <ul class="sitemap-list">
  {%- for c in site.teaching -%}
    {%- if c.sitemap == false %}{% continue %}{% endif -%}
    <li><a href="{{ c.url | relative_url }}">{{ c.title }}</a></li>
  {%- endfor -%}
  </ul>
</div>
{%- endif -%}

{%- if site.portfolio and site.portfolio != empty -%}
<div class="sitemap-section" id="portfolio">
  <h2>Portfolio</h2>
  <ul class="sitemap-list">
  {%- for item in site.portfolio -%}
    {%- if item.sitemap == false %}{% continue %}{% endif -%}
    <li><a href="{{ item.url | relative_url }}">{{ item.title }}</a></li>
  {%- endfor -%}
  </ul>
</div>
{%- endif -%}

<p class="sitemap-muted">Prefer the machine version? See the <a href="{{ base_path }}/sitemap.xml">XML sitemap</a>.</p>