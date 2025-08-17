---
layout: single
title: "Travel"
permalink: /travel/
author_profile: true
---
> *To see the world, things dangerous to come to, to see behind walls, draw closer, to find each other, and to feel. That is the purpose of life.*  
> — *The Secret Life of Walter Mitty*

One of my favorite quotes from film as it captures the spirit of curiosity, exploration, and living the moment that drives both my work and travels.
So, besides researching sleep and circadian rhythms (and staring at screens most of the day), I also love wandering and exploring the world whenever I can.

### ✈️ Favorite Place
**Hong Kong**
Home Kong! My favourite place will always be Hong Kong — it's where I grew up, and it still feels like the centre of my world. 
It may be small, but it has everything: amazing food, a buzzing city life, quiet nature trails, beaches, and hidden corners full of character.
Most importantly, it’s where my family and closest friends are.

### 🧳 Travel and Research
I'm grateful that my work often takes me places — whether it's for conferences, exchange visits, or research collaborations. It’s a privilege when academic life and travel intersect.

### 📸 A Few Moments

<div class="photo-album">
  {% for item in site.data.travel_gallery %}
    <div class="photo-card">
      <a href="/images/travel/{{ item.file }}" target="_blank">
        <img src="/images/travel/{{ item.file }}" alt="{{ item.title }} - {{ item.caption }}">
      </a>
      <div class="caption">
        <div class="caption-title">{{ item.title }}</div>
        <div class="caption-sub">{{ item.caption }}</div>
      </div>
    </div>
  {% endfor %}
</div>

---
Thanks for stopping by!  
If you have any travel recommendations or just want to chat about good food and wine, hidden beaches, SCUBA diving, or anything travel related — feel free to [drop me an email](mailto:contact@forrestcheung.com).