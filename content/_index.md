---
title: Software As Craft
description: "Thoughts on how we build software, and the effects on our industry."
cascade:
  type: page
content_blocks:
  - _bookshop_name: articles
    hide-empty: false
    heading:
      title: "Applying our craft..."
    input:
      section: posts
      sort: date
      reverse: true
      nested: true
    cols: 4
    padding: "2"
    header-style: "publication"
    footer-style: "tags"
    orientation: "stacked"
    class: "border-1 card-zoom"
    limit: 8
  - _bookshop_name: articles
    hide-empty: false
    heading:
      title: "Developing with ADHD"
    input:
      section: adhd
      sort: date
      reverse: false
      nested: true
    cols: 3
    padding: "2"
    header-style: "publication"
    footer-style: "tags"
    orientation: "stacked"
    class: "border-1 card-zoom"
    limit: 8
  - _bookshop_name: articles
    hide-empty: false
    heading:
      title: "Talks I give..."
    input:
      section: talks
      sort: date
      reverse: true
      nested: true
    cols: 4
    padding: "2"
    header-style: "full"
    footer-style: "none"
    orientation: "stacked"
    class: "border-1 card-zoom"
    limit: 8
  - _bookshop_name: articles
    hide-empty: false
    heading:
      title: "Workshops available..."
    input:
      section: workshops
      sort: date
      reverse: true
      nested: true
    cols: 4
    padding: "2"
    header-style: "full"
    footer-style: "none"
    orientation: "stacked"
    class: "border-1 card-zoom"
    limit: 8
---