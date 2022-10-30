---
layout: post
title: A longer Project Title
description: short project description
---

Example modified from [here](http://www.unexpected-vortices.com/sw/rippledoc/quick-markdown-example.html){:target="_blank"}.


{function setup() { createCanvas(600, 600); strokeWeight(2); resetSketch(); }

function resetSketch() { spooks = [];

for (let i = 0; i < 3; i++) { spooks.push(new Spook()); } }

function draw() { background(0);

if (noise(frameCount* 0.02) < 0.3) { lightning(); }

if (((frameCount + 180) % 360) == 0) { random(spooks).startWooing(true); }

spooks.forEach(s => s.draw()); }

function lightning() { push(); stroke(255); strokeJoin(MITER); let x = width * 0.1 + random(width * 0.8); let y = 0; let steps = random(30, 80); for (let i = 0; i < steps; i++) { strokeWeight(random(3, 6)); let x1 = x + random(-20, 20); let y1 = y + random(-10, 20); line(x, y, x1, y1); x = x1; y = y1; } pop(); }

class Spook { constructor() { this.scale = random(0.005, 0.02); this.scalePhase = random(360);
}