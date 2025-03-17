---
draft: true
date: '{{ .Date }}'
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
description: "Desc Text."
tags: ["tag1", "tag2", "tag3"]
seo_keywords: "Sharfuddin Shawon, Portfolio"
showToc: true
TocOpen: false
hideSummary: false
searchHidden: false
ShowBreadCrumbs: true
# slug: "{{ .Slug }}"
# aliases: ["/{{ .Slug }}"]
# canonicalURL: 'https://shawon.me/projects/{{ replace .File.ContentBaseName "-" " " | title }}'
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
---