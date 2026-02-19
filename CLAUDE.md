# HACK.SIM Development Guide

## Project Overview
Text-only (ASCII) browser hacker-themed hack-and-slash game. Single `index.html` file, vanilla JS, no frameworks.

## Constraints
- **NO emoji, NO unicode symbols** — use plain ASCII text only (e.g., `[+]` not ▲, `>` not ▶, `*` not ×)
- Mouse-only controls (move to aim, click/hold to attack)
- Single HTML file — all CSS, JS inline
- No defeat condition — infinite scaling, player-controlled MapLv difficulty
- Player is a "destructive weapon" adding parts (not a human character)

## Architecture
- State object: `state.equipped = {cores:[x4], subs:[x4], modules:[x4]}`
- 3 equipment categories: CORE (click attack shape), SUB (auto-attack mode), MODULE (affix-only stats)
- CORE shapes: circle, line, cone, nova, pierce-burst, lock-on
- SUB modes: nearest, chain, explode, orbit, parasite, drone
- Credits currency, upgrade shop with exponential cost scaling
- `getComputedStats()` aggregates all equipment stats

## CRITICAL: Enemy Movement
The `updateEnemies()` function uses center-pull physics:
- Pull toward center: `40 * dt`
- Damping: `0.97`
- Edge bounce redirects toward center
- Gentle inter-enemy repulsion
**DO NOT replace this with random-walk or other movement patterns.**

## Style
- Terminal/hacker aesthetic: black background (#0a0a0a), green text (#00ff41)
- Rarity colors: common=#aaa, uncommon=#00ff41, rare=#4488ff, epic=#aa44ff, legendary=#ffaa00, unique=#ff2222
- All item names displayed as `[iLN] ItemName`
