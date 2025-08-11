---
title: "Personal Website & Blog"
date: 2025-01-11T12:00:00-00:00
draft: false
description:
  "A modern, fast personal website built with Hugo and the Blowfish theme"
tags: ["hugo", "web-development", "static-site", "github-pages"]
categories: ["web"]
---

## Overview

This personal website serves as both a portfolio and blog, showcasing my
projects and sharing technical insights. Built with modern web technologies for
optimal performance and maintainability.

## Tech Stack

- **Hugo**: Static site generator for fast builds and excellent performance
- **Blowfish Theme**: Modern, responsive Hugo theme with extensive customization
- **GitHub Pages**: Free hosting with automatic deployment
- **GitHub Actions**: CI/CD pipeline for automated builds and deployments
- **Markdown**: Content creation with simple, version-controlled markup

## Features

- 📱 **Responsive Design**: Works perfectly on desktop, tablet, and mobile
- 🌙 **Dark Mode**: Automatic theme switching based on user preference
- 🔍 **Search**: Built-in search functionality for easy content discovery
- ⚡ **Fast Loading**: Optimized static site with minimal JavaScript
- 📊 **SEO Optimized**: Structured data and meta tags for better search
  visibility
- 🔄 **Auto Deployment**: Push to main branch triggers automatic deployment

## Architecture

```
jmccrystal.github.io/
├── content/          # Markdown content files
│   ├── posts/        # Blog posts
│   ├── projects/     # Project showcases
│   └── about.md      # About page
├── themes/blowfish/  # Hugo theme (git submodule)
├── hugo.toml         # Site configuration
└── .github/workflows/ # GitHub Actions CI/CD
```

## Deployment Pipeline

The site uses GitHub Actions for continuous deployment:

1. **Trigger**: Push to main branch
2. **Build**: Hugo generates static files
3. **Deploy**: Files deployed to GitHub Pages
4. **Live**: Site available at `https://jmccrystal.github.io`

## Key Learnings

- Hugo's build speed is exceptional for static site generation
- Git submodules work well for theme management
- GitHub Pages integration is seamless with proper Actions setup
- The Blowfish theme offers extensive customization without complexity

## Links

- 🌐 [Live Site](https://jmccrystal.github.io)
- 📁 [Source Code](https://github.com/jmccrystal/jmccrystal.github.io)
- 🎨 [Blowfish Theme](https://themes.gohugo.io/themes/blowfish/)

---

_This project demonstrates modern static site development practices and serves
as a template for similar projects._
