---
layout: single
title: "Travel"
permalink: /travel/
author_profile: true
---
> *To see the world, things dangerous to come to, to see behind walls, draw closer, to find each other, and to feel. That is the purpose of life.*  
> — *The Secret Life of Walter Mitty*

One of my favorite quotes from film as it captures the spirit of curiosity, exporation, and living the moment that drives both my work and travels.
So, besides researching sleep and circadian rhythms (and staring at screens most of the day), I also love wandering and exploring the world whenever I can.

### 🧳 Travel and Research
I'm grateful that my work often takes me places — whether it's for conferences, exchange visits, or research collaborations. It’s a privilege when academic life and travel intersect.

### ✈️ Favorite Places
- **Hong Kong (Home!)** – Home Kong! It has everything — world-class food, nonstop energy, and of course where my friends and family are. How could I not love this place?
- **Iceland** – Otherworldly landscapes, geothermal magic, and a front-row seat to the northern lights.
- **Greece** – Steeped in culture and mythology, with island-hopping across the Aegean Sea.
- **Easter Island** – Remote and full of mystery. The Moai, the silence, and the Polynesian heritage left a lasting impression.
  
### 📸 A Few Moments

<div class="photo-album">
  {% for item in site.data.travel_gallery %}
    <div class="photo-card">
      <a href="/images/travel/{{ item.file }}" target="_blank">
        <img src="/images/travel/{{ item.file }}" alt="{{ item.caption }}">
      </a>
      <div class="caption">{{ item.caption }}</div>
    </div>
  {% endfor %}
</div>
---
Thanks for stopping by!  
If you have any travel recommendations or just want to chat about good food and wine, hidden beaches, SCUBA diving, or anything travel related — feel free to [drop me an email](mailto:forrestcheungtw@gmail.com).