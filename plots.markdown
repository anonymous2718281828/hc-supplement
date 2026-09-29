---
title: Additional Plots
layout: default
---

# About this page

This page contains additional plots.

## RQ 1

The following plot shows a full version, including all case studies, of the plot used in Table 4.

![](/images/rq1-all.svg)


{% for project in site.data.projects %}
# {{ project.name }}

## RQ2.1: In-Setting Differences

<div class="image-container">
  <img src="images/{{ project.name | downcase }}-rq21.svg" alt="">
</div>

## RQ2.2: In-Alternative Differences

<div class="image-container">
  <img src="images/{{ project.name | downcase }}-rq22.svg" alt="">
</div>

{% endfor %}
