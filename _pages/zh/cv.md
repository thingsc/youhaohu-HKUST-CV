---
layout: page
permalink: /zh/cv/
title: 简历
lang: zh-CN
alternate_url: /cv/
description: Youhao Hu 的中文简历。
nav: true
nav_order: 5
cv_pdf: /assets/pdf/youhao-hu-cv-zh.pdf
toc:
  sidebar: left
---

{% assign cv = site.data.cv_zh.cv %}

<div class="cv">
  <div class="cv-download mb-4">
    <a class="btn btn-sm z-depth-0" href="{{ page.cv_pdf | relative_url }}" target="_blank" rel="noopener noreferrer">下载中文 PDF 简历</a>
  </div>

  <header class="post-header">
    <h1 class="post-title">{{ cv.name }}</h1>
    <p class="desc">{{ cv.summary }}</p>
    <p>
      {{ cv.location }}
      <br>
      <a href="mailto:{{ cv.email }}">{{ cv.email }}</a>
      {% if cv.phone %}
        <br>{{ cv.phone }}
      {% endif %}
    </p>
  </header>

{% for section in cv.sections %}

<h2 id="{{ section[0] }}">{{ section[0] }}</h2>
{% for item in section[1] %}
<div class="cv-entry">
<div class="d-flex justify-content-between flex-wrap">
<h3>{{ item.institution | default: item.company | default: item.title | default: item.name }}</h3>
<span class="cv-date">
{% if item.start_date or item.end_date %}
{{ item.start_date }}{% if item.end_date %} - {{ item.end_date }}{% endif %}
{% elsif item.date %}
{{ item.date }}
{% elsif item.releaseDate %}
{{ item.releaseDate }}
{% endif %}
</span>
</div>

        {% if item.studyType or item.area or item.position or item.publisher or item.level %}
          <p class="cv-meta">
            {{ item.studyType | default: item.position | default: item.publisher | default: item.level }}
            {% if item.area %} · {{ item.area }}{% endif %}
          </p>
        {% endif %}

        {% if item.location %}
          <p class="cv-meta">{{ item.location }}</p>
        {% endif %}

        {% if item.authors %}
          <p class="cv-meta">{{ item.authors | join: ", " }}</p>
        {% endif %}

        {% if item.awarder %}
          <p class="cv-meta">{{ item.awarder }}</p>
        {% endif %}

        {% if item.summary %}
          {{ item.summary | markdownify }}
        {% endif %}

        {% if item.keywords %}
          <p>{{ item.keywords }}</p>
        {% endif %}

        {% if item.highlights and item.highlights.size > 0 %}
          <ul>
            {% for highlight in item.highlights %}
              <li>{{ highlight | markdownify | remove: '<p>' | remove: '</p>' }}</li>
            {% endfor %}
          </ul>
        {% endif %}
      </div>
    {% endfor %}

{% endfor %}

</div>
