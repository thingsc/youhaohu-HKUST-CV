---
layout: cv_zh
permalink: /zh/cv/
title: 简历
lang: zh-CN
alternate_url: /cv/
description:
nav: true
nav_order: 5
cv_pdf: /assets/pdf/youhao-hu-cv-zh.pdf
# cv_pdf: https://github.com/thingsc/youhaohu-CV-PDF-cn/releases/download/v1.0/youhaohu-CV-CN.pdf
toc:
  sidebar: left
---

{% assign cv = site.data.cv_zh.cv %}

<div class="cv">
  <header class="post-header cv-profile-header">
    <h1 class="post-title">{{ cv.name }}</h1>
    <p class="desc">{{ cv.summary }}</p>
  </header>

  <section class="cv-section-card cv-contact-card card mt-3 p-3">
    <h2 id="联系信息" class="card-title font-weight-medium">联系信息</h2>
    <table class="table table-cv table-sm table-borderless mb-0">
      <tr>
        <td class="p-1 pr-2 font-weight-bold"><b>姓名</b></td>
        <td class="p-1 pl-2 font-weight-light">{{ cv.name }}</td>
      </tr>
      <tr>
        <td class="p-1 pr-2 font-weight-bold"><b>邮箱</b></td>
        <td class="p-1 pl-2 font-weight-light"><a href="mailto:{{ cv.email }}">{{ cv.email }}</a></td>
      </tr>
      {% if cv.phone %}
        <tr>
          <td class="p-1 pr-2 font-weight-bold"><b>电话</b></td>
          <td class="p-1 pl-2 font-weight-light">{{ cv.phone }}</td>
        </tr>
      {% endif %}
      <tr>
        <td class="p-1 pr-2 font-weight-bold"><b>所在地</b></td>
        <td class="p-1 pl-2 font-weight-light">{{ cv.location }}</td>
      </tr>
    </table>
  </section>

{% for section in cv.sections %}

    <section class="cv-section-card card mt-3 p-3">
      <h2 id="{{ section[0] }}" class="card-title font-weight-medium">{{ section[0] }}</h2>
      {% for item in section[1] %}
        <div class="cv-entry">
          <div class="d-flex justify-content-between flex-wrap">
            <h4 class="cv-entry-title">{{ item.institution | default: item.company | default: item.title | default: item.name }}</h4>
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
    </section>

{% endfor %}

</div>
