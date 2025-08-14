---
layout: single
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

{%- assign pubs = site.publications | default: site.collections.publications.docs -%}
{%- if pubs and pubs != empty -%}
<div class="sitemap-section" id="publications">
  <h2>Publications</h2>

  {%- comment -%}
  Build a flat, newest→oldest list.
  We prioritize items with a full `date`, then items with only `year`,
  then anything without either (at the end). We only skip items with `published: false`.
  Remove that check if you truly want *everything*, including drafts.
  {%- endcomment -%}
  {%- assign with_date = "" | split:"" -%}
  {%- assign year_only = "" | split:"" -%}
  {%- assign no_when   = "" | split:"" -%}

  {%- for p in pubs -%}
    {%- if p.published == false %}{% continue %}{% endif -%}
    {%- if p.date -%}
      {%- assign with_date = with_date | push: p -%}
    {%- elsif p.year -%}
      {%- assign year_only = year_only | push: p -%}
    {%- else -%}
      {%- assign no_when = no_when | push: p -%}
    {%- endif -%}
  {%- endfor -%}

  {%- assign with_date  = with_date  | sort: "date" | reverse -%}
  {%- assign year_only  = year_only  | sort: "year" | reverse -%}
  {%- assign pubs_sorted = with_date | concat: year_only | concat: no_when -%}

  <ul class="sitemap-list">
    {%- for p in pubs_sorted -%}
      <li>
        <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
        {%- if p.date -%}
          <span class="sitemap-muted"> — {{ p.date | date: "%Y-%m-%d" }}</span>
        {%- elsif p.year -%}
          <span class="sitemap-muted"> — {{ p.year }}</span>
        {%- endif -%}
      </li>
    {%- endfor -%}
  </ul>
</div>
{%- endif -%}

{%- assign talks = site.talks | default: site.collections.talks.docs -%}
{%- if talks and talks != empty -%}
<div class="sitemap-section" id="talks">
  <h2>Talks</h2>

  {%- comment -%} Split by available date info {%- endcomment -%}
  {%- assign with_date = "" | split:"" -%}
  {%- assign year_only = "" | split:"" -%}
  {%- assign no_when   = "" | split:"" -%}

  {%- for t in talks -%}
    {%- if t.published == false %}{% continue %}{% endif -%}
    {%- if t.date -%}
      {%- assign with_date = with_date | push: t -%}
    {%- elsif t.year -%}
      {%- assign year_only = year_only | push: t -%}
    {%- else -%}
      {%- assign no_when = no_when | push: t -%}
    {%- endif -%}
  {%- endfor -%}

  {%- assign with_date   = with_date  | sort: "date" | reverse -%}
  {%- assign year_only   = year_only  | sort: "year" | reverse -%}
  {%- assign talks_sorted = with_date | concat: year_only | concat: no_when -%}

  <ul class="sitemap-list">
    {%- for t in talks_sorted -%}
      <li>
        <a href="{{ t.url | relative_url }}">{{ t.title }}</a>
        {%- if t.date -%}
          <span class="sitemap-muted"> — {{ t.date | date: "%Y-%m-%d" }}</span>
        {%- elsif t.year -%}
          <span class="sitemap-muted"> — {{ t.year }}</span>
        {%- endif -%}
        {%- if t.venue %} <span class="sitemap-muted"> — {{ t.venue }}</span>{% endif -%}
      </li>
    {%- endfor -%}
  </ul>
</div>
{%- endif -%}

{%- if site.posts and site.posts != empty -%}
<div class="sitemap-section" id="posts">
  <h2>News & Updates</h2>

  {%- assign posts_sorted = site.posts 
    | where_exp: "p", "p.published != false" 
    | sort: "date" 
    | reverse -%}

  <ul class="sitemap-list">
    {%- for post in posts_sorted -%}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span class="sitemap-muted"> — {{ post.date | date: "%Y-%m-%d" }}</span>
      </li>
    {%- endfor -%}
  </ul>
</div>
{%- endif -%}

<p class="sitemap-muted">Prefer the machine version? See the <a href="{{ base_path }}/sitemap.xml">XML sitemap</a>.</p>
