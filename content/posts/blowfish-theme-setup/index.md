---
title: "Setting Up the Blowfish Theme for Hugo"
date: 2025-01-11T14:00:00-00:00
draft: false
description: "A comprehensive guide to setting up and customizing the Blowfish theme for your Hugo site."
tags: ["hugo", "blowfish", "themes", "web-design"]
categories: ["web-development"]
---

The Blowfish theme is a powerful, modern Hugo theme that offers extensive customization options and a clean, professional appearance. Here's how I set it up for this site.

## Why Blowfish?

Blowfish stands out for several reasons:

- **Modern Design**: Clean, responsive layouts that work well on all devices
- **Extensive Configuration**: Highly customizable without touching code
- **Multiple Layout Options**: Profile, hero, card, and background layouts
- **Built-in Features**: Search, dark mode, social links, and more
- **Performance**: Optimized for speed and SEO

## Installation

Installing Blowfish is straightforward using Git submodules:

```bash
# Remove existing theme (if any)
git submodule deinit -f themes/oldtheme
rm -rf themes/oldtheme

# Add Blowfish as a submodule
git submodule add https://github.com/nunocoracao/blowfish.git themes/blowfish
```

## Configuration Highlights

Here are some key configuration options I used:

### Basic Setup
```toml
theme = 'blowfish'
enableEmoji = true

[params]
  colorScheme = "blowfish"
  defaultAppearance = "light"
  autoSwitchAppearance = true
```

### Homepage Layout
```toml
homepage.layout = "profile"
homepage.showRecent = true
homepage.showRecentItems = 5
```

### Navigation Menu
```toml
[[menus.main]]
  name = "Posts"
  pageRef = "/posts"
  weight = 10

[[menus.main]]
  name = "Projects"
  pageRef = "/projects"
  weight = 20
```

## Author Profile

One of Blowfish's standout features is the author profile section:

```toml
[params.author]
  name = "James McCrystal"
  image = "https://avatars.githubusercontent.com/u/30939190"
  headline = "Software Engineer & Technology Enthusiast"
  bio = "Passionate about building great software and sharing knowledge through writing."
```

The theme automatically creates a beautiful profile section with your image, bio, and social links.

## Tips for Customization

1. **Use the Profile Layout**: Perfect for personal sites and blogs
2. **Enable Search**: The built-in search functionality is fast and effective
3. **Configure Social Links**: Easy to add GitHub, LinkedIn, Twitter, etc.
4. **Customize Colors**: The color scheme is easily adjustable
5. **Enable Dark Mode**: Automatic switching based on user preference

## Conclusion

Blowfish offers an excellent balance of features and simplicity. The extensive configuration options mean you can create a unique site without writing custom code, while the clean codebase makes customization straightforward when needed.

The theme's focus on performance and accessibility makes it an excellent choice for professional websites and personal blogs alike.