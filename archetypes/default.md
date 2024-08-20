---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
draft: true
slug: '{{ .File.ContentBaseName | replace "-" " " | lower | urlize }}'
---
