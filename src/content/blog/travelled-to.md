---
title: 'travelled.to - a travel map in an evening'
description: 'Building a shareable travel map with Claude when no free alternative existed'
pubDate: 2025-01-13
heroImage: '../../assets/travelled-to.png'
---

https://travelled.to/

I wanted to share a map of my recent travels with friends. The kind with elegant arrows connecting cities, perfect for an Instagram story. Surely there's a free tool for this?

There isn't. Or at least, nothing that felt right. The options were either paywalled, cluttered with ads, or required creating accounts for features I'd use once or twice per year.

So I built one in an evening with Claude.

## The Stack

- **Vue 3** with Composition API and TypeScript
- **Mapbox GL** for the base map
- **Deck.gl** for WebGL-powered curved arrows
- **Pinia** for state management
- **Tailwind** for quick styling

The whole thing runs client-side. The stack I've already built with, see https://www.kada.lv/#/darijumi.

## What It Does

Type a city name, the app geocodes it and drops a marker. Add more cities, and a line traces your journey. Switch between curved arcs or straight lines. Pick from different map styles. Adjust colors, opacity, marker sizes.

When you're happy with the result, export it. The share button copies a caption and opens the selected app on mobile. Everything saves to localStorage, so your trip persists between sessions.

## Building It

I used Claude to speed things up. Describe a feature, get code, tweak it, repeat. Figuring out the Deck.gl arc layer setup and canvas export quirks were the fiddly parts. Two years ago I would spend close to a week on this.

## Try It

https://travelled.to/

Sometimes the best tool is the one you build yourself.
