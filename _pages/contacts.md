---
layout: contacts
title: contacts
permalink: /contacts/
description: 
nav: true
nav_order: 4
---
<div class="members clearfix">
  {% for member in site.data.contacts.Active %}
  <div class="member-profile-two-col">
    <a href="{{ member.url }}" target="_blank"><img src="{{ member.image | prepend: '/assets/img/' | relative_url }}" /></a>
    <ul class="member-info">
      <li><span>Name:</span> <a href="{{ member.url }}" target="_blank">{{ member.name }}</a></li>
      <li><span>Institute:</span> {{ member.institute }}</li>
      <li><span>Email:</span> <a href="mailto:{{ member.email | encode_email }}" target="_blank">{{ member.email }}</a></li>
      {%- if member.field -%}
        {%- assign field_list = member.field | split: ", " -%}
        {%- for field in field_list -%}
          {%- if site.data.venues[field] -%}
            {%- assign venue_style = nil -%}
            {%- if site.data.venues[field].color != blank -%}
              {%- assign venue_style = site.data.venues[field].color | prepend: 'style="background-color:' | append: '"' -%}
            {%- endif -%}
            <abbr class="badge" {% if venue_style %}{{venue_style}}{% endif %}>{{field}}</abbr> &nbsp;
          {%- else -%}
            <abbr class="badge">{{field}}</abbr> &nbsp; 
          {%- endif -%}
        {%- endfor -%}
      {%- endif -%}
    </ul>
  </div>
  {% endfor %}
</div>

