---
title: Additional Plots
layout: default
---

# About this page

This page contains additional and detailed plots for RQ2.1 and RQ2.2


{% for project in site.data.projects %}
# {{ project.name }}

## RQ2.1: In-Setting Differences

![](images/{{ project.name | downcase }}-rq21.svg)

## RQ2.2: In-Alternative Differences

![](images/{{ project.name | downcase }}-rq22.svg)

{% endfor %}
