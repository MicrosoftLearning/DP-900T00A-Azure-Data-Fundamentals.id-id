---
title: Instruksi yang Tersedia Online
permalink: index.html
layout: home
---

# Latihan Dasar-Dasar Data Azure

Latihan langsung ini dirancang untuk mendukung konten pelatihan di [Microsoft Learn](https://docs.microsoft.com/training/).

Untuk menyelesaikan latihan ini, Anda harus berlangganan Microsoft Azure dengan izin administratif. Anda dapat mendaftar untuk uji coba gratis di [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Latihan |
| --- |
{% untuk aktivitas di lab %}| [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
