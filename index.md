---
title: Petunjuk Host Online
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: id-ID
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682426"
---
# <a name="azure-data-fundamentals-exercises"></a>Latihan Dasar-Dasar Data Azure

Gunakan tautan di bawah untuk menyelesaikan latihan lab langsung untuk kursus Microsoft [DP-900 *Dasar-Dasar Data Microsoft Azure*](https://docs.microsoft.com/learn/certifications/courses/dp-900t00).

Untuk menyelesaikan latihan ini, Anda harus berlangganan Microsoft Azure Jika instruktur Anda belum menyediakannya, Anda dapat mendaftar untuk coba gratis di [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url berisi '/Instructions/Labs'" %}
| Modul | Laboratorium |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
