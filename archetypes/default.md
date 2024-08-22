---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
draft: true
categories: 
slug: '{{ .File.ContentBaseName | replace "-" " " | lower | urlize }}'
---
