# Pixel Fisher

A small pixel-art fishing game that runs in the browser. You sit in a boat at
sunset, cast a line with the mouse, hook a fish and reel it in by passing three
quick keyboard challenges before it gets away.

## What it is

A weekend-sized game built in April 2026 with Next.js and a single HTML canvas.
Everything on screen (sky gradient, clouds, birds, sea, mountains, boat, rod,
fish) is drawn frame by frame in `components/GameCanvas.tsx`; the PNG sprites in
`public/` are the only art assets.

The input layer was written as an interface (`GameInput`) so the game could later
be driven by hand tracking (pinch to cast, and so on) instead of a mouse. Only the
keyboard and mouse implementation exists in this repo; the game is fully playable
with it.

## How it works

- An intro screen plays a short looping video; any key or click dismisses it and
  starts the game.
- The rod follows the mouse. A click casts the line along a bezier arc; if nothing
  bites it retracts on its own.
- One fish swims at a time, bouncing between the mountains at 40 to 70 px/s. If the
  hook lands close enough, the fish is hooked and the reeling phase starts.
- Reeling is three challenges in a row, each with a 6 second timer and picked at
  random from: press the shown digit, hold Space for 2 seconds, or mash F eight
  times. Each one pulls the fish a third of the way to the rod. Fail a timer and
  the fish escapes.
- Landing a fish adds 100 to the score shown in the top-left corner.

## Stack

Next.js 14 (App Router), React 18, TypeScript, Tailwind for the page shell, raw
Canvas 2D for the game. The pixel font is Press Start 2P from Google Fonts.

## Run it

```bash
npm ci
npm run dev      # http://localhost:3000
npm run build    # production build
```

## Project layout

```
app/          Next.js entry: layout, intro screen (page.tsx), global styles
components/   GameCanvas.tsx, the whole game loop and renderer
lib/game/     FishManager: spawning, swimming, hook/catch state
lib/input/    GameInput interface and the keyboard+mouse implementation
public/       sprites (boat, fish, mountains, clouds, distant boat) and intro video
```

## Team

- Luis Molina Salvador ([34lumo](https://github.com/34lumo)): game, rendering, input layer
- [marcusen78-sketch](https://github.com/marcusen78-sketch): intro screen with video
