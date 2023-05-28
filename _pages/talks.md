---
layout: schedule
permalink: /talks/
title: Physics
nav: true
nav_order: 1
---
{% assign prev_date = 0 %}

{% for item in site.data.lectures %}
{% if item.date %}
{% assign lecture = item %}
{% assign event_type = "upcoming" %}
{% assign today_date = "now" | date: "%s" | divided_by: 86400 %}
{% assign lecture_date = lecture.date | date: "%s" | divided_by: 86400 %}
{% if today_date > lecture_date %}
    {% assign event_type = "past" %}
{% elsif today_date <= lecture_date and today_date > prev_date %}
    {% assign event_type = "warning" %}
{% endif %}
{% assign prev_date = lecture_date %}

<tr class="{{ event_type }}">
    <th scope="row">{{ lecture.date }}</th>
    <td>
        {{ lecture.title }}
    </td>
    <td>
        {% if lecture.speaker %}
        Speaker: <i>{{ lecture.speaker }}</i>
        {% endif %}
        <!--
        {% if lecture.institute %}
        ({{ lecture.institute}})
        {% endif %}
        -->
    </td>
    <td>
         {% if lecture.slides %}
         <a href="{{ lecture.slides }}" target="_blank">slides</a>
         {% endif %}
    </td>
</tr>
{% else %}
{% assign module = item %}
<tr class="table-active">
    <td colspan="5" align="center"><strong>{{ module.title }}</strong></td>
</tr>
{% endif %}
{% endfor %}
