---
draft: true
date: '{{ .Date }}'
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
description: "Desc Text."
# aliases: ["/first"]
tags: ["tag1", "tag2", "tag3"]
showToc: true
TocOpen: false
hideSummary: false
searchHidden: false
ShowBreadCrumbs: true
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
---