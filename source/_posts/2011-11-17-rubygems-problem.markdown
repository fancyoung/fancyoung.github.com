---
layout: post
title: "Ruby on Rails使用时灵异的Bug"
date: 2011-11-17 20:33
comments: true
categories: [Ruby]
---
> 送给敬爱的GFW

## 问题
`$ rails new`报错  
`$ bundle install`报错  
等等一切灵异问题  
据说是因为rubygems.org用的是Amazon的S3服务，而部分s3服务器被GFW拦于墙外。

## 解决
- 2012.12.31更新：淘宝提供了镜像  
`$ gem sources -a http://ruby.taobao.org/`

- 曾经解决方案，单独下载安装包  
  可能需要安装的包  
  multi_json  
  activesupport  

## 链接
[Rubygems](http://rubygems.org/)
