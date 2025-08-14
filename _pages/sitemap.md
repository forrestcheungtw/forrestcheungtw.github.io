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

{%- comment -%}
Avoid regex in Liquid. We'll filter utilities with simple 'contains' checks
and by comparing the last path segment (slug).
{%- endcomment -%}
{%- assign exclude_slug_list = "404,talkmap" | split: "," -%}

<div class="sitemap-section" id="pages">
  <h2>Pages</h2>
  <ul class="sitemap-list">
  {%- comment -%}
    We can't safely use 'concat' if a collection is missing, so loop each source.
    1) site.html_pages
    2) _pages collection if it exists
  {%- endcomment -%}

  {%- assign html_pages = site.html_pages | where_exp: "p","p.sitemap != false" -%}
  {%- for p in html_pages -%}
    {%- if p.url and p.title -%}
      {%- assign last = p.url | split:"/" | last | replace: ".html","" -%}
      {%- assign is_util = false -%}
      {%- if exclude_slug_list contains last %}{% assign is_util = true %}{% endif -%}
      {%- if p.url == "/" or p.url == page.url %}{% assign is_util = true %}{% endif -%}
      {%- if p.url contains "/categories/" or p.url contains "/tags/" or p.url contains "/page-archive/" or p.url contains "/collection-archive/" or p.url contains "/year-archive/" or p.url contains "/sitemap/" or p.url contains "/markdown/" or p.url contains "/markdown_generator/" or p.url contains "/non-menu-page/" or p.url contains "/terms/" %}{% assign is_util = true %}{% endif -%}
      {%- unless is_util -%}
        <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
      {%- endunless -%}
    {%- endif -%}
  {%- endfor -%}

  {%- if site.collections and site.collections.pages and site.collections.pages.docs -%}
    {%- assign coll_pages = site.collections.pages.docs | where_exp: "p","p.sitemap != false" -%}
    {%- for p in coll_pages -%}
      {%- if p.url and p.title -%}
        {%- assign last = p.url | split:"/" | last | replace: ".html","" -%}
        {%- assign is_util = false -%}
        {%- if exclude_slug_list contains last %}{% assign is_util = true %}{% endif -%}
        {%- if p.url == "/" or p.url == page.url %}{% assign is_util = true %}{% endif -%}
        {%- if p.url contains "/categories/" or p.url contains "/tags/" or p.url contains "/page-archive/" or p.url contains "/collection-archive/" or p.url contains "/year-archive/" or p.url contains "/sitemap/" or p.url contains "/markdown/" or p.url contains "/markdown_generator/" or p.url contains "/non-menu-page/" or p.url contains "/terms/" %}{% assign is_util = true %}{% endif -%}
        {%- unless is_util -%}
          <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
        {%- endunless -%}
      {%- endif -%}
    {%- endfor -%}
  {%- endif -%}
  </ul>
</div>

{%- if site.publications and site.publications != empty -%}
<div class="sitemap-section" id="publications">
  <h2>Publications</h2>
  {%- assign pubs = site.publications | where_exp: "p","p.sitemap != false" -%}
  {%- assign years = pubs | map:"date" | map:"year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for p in pubs -%}
        {%- if p.date -%}
          {%- assign p_year = p.date | date: "%Y" -%}
          {%- if p_year == y -%}
            <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
          {%- endif -%}
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

{%- if site.talks and site.talks != empty -%}
<div class="sitemap-section" id="talks">
  <h2>Talks</h2>
  {%- assign talks = site.talks | where_exp: "t","t.sitemap != false" -%}
  {%- assign years = talks | map:"date" | map:"year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for t in talks -%}
        {%- if t.date -%}
          {%- assign t_year = t.date | date: "%Y" -%}
          {%- if t_year == y -%}
            <li>
              <a href="{{ t.url | relative_url }}">{{ t.title }}</a>
              {%- if t.venue %} <span class="sitemap-muted">— {{ t.venue }}</span>{% endif -%}
            </li>
          {%- endif -%}
        {%- endif -%}
      {%- endfor -%}
    </ul>
  {%- endfor -%}
</div>
{%- endif -%}

{%- if site.posts and site.posts != empty -%}
<div class="sitemap-section" id="posts">
  <h2>News & Updates</h2>
  {%- assign posts = site.posts | where_exp: "p","p.sitemap != false" -%}
  {%- assign years = posts | map:"date" | map:"year" | uniq | sort | reverse -%}
  {%- for y in years -%}
    <div class="sitemap-year">{{ y }}</div>
    <ul class="sitemap-list">
      {%- for post in posts -%}
        {%- if post.date -%}
          {%- assign post_year = post.date | date: "%Y" -%}
          {%- if post_year == y -%}
            <li>
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
              <span class="sitemap-muted">— {{ post.date | date: "%b %d" }}</span>
            </li>
          {%- endif -%}
        {%- endif -%}
      {%- endfor -%}
    </ul>
  {%- endfor -%}
</div>
{%- endif -%}

<p class="sitemap-muted">Prefer the machine version? See the <a href="{{ base_path }}/sitemap.xml">XML sitemap</a>.</p>
