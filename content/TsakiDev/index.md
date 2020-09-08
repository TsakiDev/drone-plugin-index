---
version: '1.1.0'
date: 2020-09-08T00:00:00+00:00
title: Gitea Comment
author: TsakiDev
tags: [ gitea ]
logo: gitea.svg
repo: tsakidev/giteacomment
image: tsakidev/giteacomment
---

A Drone plugin to post comments on a Gitea Pull Request. The below pipeline configuration demonstrates simple usage:

Example reference for pull request with static string:

```yml
steps:
- name: post-to-gitea-pr
  image: tsakidev/giteacomment:latest
  settings:
    gitea_token:
      from_secret: gitea_token
    gitea_base_url: http://gitea.example.com
    comment: "Hello from Drone"
  when:
    status: [ failure ]
    event: pull_request
```

Example reference for pull request with input from file:

```yml
steps:
- name: post-to-gitea-pr
  image: tsakidev/giteacomment:latest
  settings:
    gitea_token:
      from_secret: gitea_token
    gitea_base_url: http://gitea.example.com
    comment_title: "My Title"
    comment_from_file: "/path/to/file.txt"
  when:
    status: [ failure ]
    event: pull_request
```

# Secret Reference

gitea_token
: gitea access token

# Parameter Reference

gitea_base_url
: gitea base url

comment_title (optional)
: h2 comment title, only works if comment_from_file exists

comment or comment_from_file
: the string to post to gitea or the path of the file to read (overrides comment is exists)
