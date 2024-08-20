---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: {{ .Date }}
draft: true
categories: Java
slug: '{{ .File.ContentBaseName | replace "-" " " | lower | urlize }}'
---
