---
title: Configuration Alternatives
---

This page provides information for all configuration alternatives used in our evaluation.
In addition, we provide the patches used for configuration opportunities. The patches contain placeholders as accepted by [jinja](https://jinja.palletsprojects.com/en/stable/) to dynamically generate patches for different values.

**Note:** There might be patches for configuration alternatives that are not mentioned in the mapping. This can happen when all configuration alternatives are not used in the evaluation, e.g., because they did not pass test suites.


{% for project in site.data.projects %}
# {{ project.name }}

## Alternatives
{% for alternative in project.conf_alts %}


### `{{ alternative }}`

```patch
{% include {{ project.name | downcase }}/{{ alternative }}.patch %}
```
{% endfor %}

## Configuration Alternative ID Mapping

<details style="background:#d3d3d3;border-left:5px solid #a9a9a9;padding:0.75em;border-radius:4px;">
  <summary style="font-weight:bold;cursor:pointer;">
    Click to show
  </summary>

    {% include {{ project.name | downcase }}/confalts.html %}

</details>

{% endfor %}
