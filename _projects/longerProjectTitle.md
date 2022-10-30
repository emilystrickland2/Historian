---
layout: post
title: A longer Project Title
description: short project description
---

Example modified from [here](http://www.unexpected-vortices.com/sw/rippledoc/quick-markdown-example.html){:target="_blank"}.




let spooks = [];

function setup() {
  createCanvas(600, 600);
  strokeWeight(2);
  resetSketch();
}

function resetSketch() {
  spooks = [];

  for (let i = 0; i < 3; i++) {
    spooks.push(new Spook());
  }
}

function draw() {
  background(0);

  if (noise(frameCount* 0.02) < 0.3) {
    lightning();
  }
  
  if (((frameCount + 180) % 360) == 0) {
    random(spooks).startWooing(true);
  }

  spooks.forEach(s => s.draw());
}

function lightning() {
  push();
  stroke(255);
  strokeJoin(MITER);
  let x = width * 0.1 + random(width * 0.8);
  let y = 0;
  let steps = random(30, 80);
  for (let i = 0; i < steps; i++) {
    strokeWeight(random(3, 6));
    let x1 = x + random(-20, 20);
    let y1 = y + random(-10, 20);
    line(x, y, x1, y1);
    x = x1; y = y1;
  }
  pop();
}

class Spook {
  constructor() {
    this.scale = random(0.005, 0.02);
    this.scalePhase = random(360);
    
    this.moveX = random(0.005, 0.019);
    this.moveY = random(0.005, 0.01);
    this.movePhase = random(360);
    
    this.sway0 = random(0, 0.04);
    this.sway2 = random(0, 0.04);
    
    this.pt = [
      createVector(0, 160),
      createVector(60, 0),
      createVector(120, 160)
      ];
    this.cp = [
      createVector(0, 40),
      createVector(20, 0),
      createVector(100, 0),
      createVector(120, 40)
    ];
    
    this.pt0 = this.pt[0];
    this.pt2 = this.pt[2];
    
    this.woo = "";
  }
  
  draw() {
    push();

    scale(map(sin((frameCount + this.scalePhase) * this.scale), -1, 1, 0.7, 1));
    translate(map(cos((frameCount + this.movePhase) * this.moveX), 1, -1, 0, 420),
              map(cos((frameCount + this.movePhase) * this.moveY), 1, -1, 0, 420));

    this.pt[0] = p5.Vector.add(this.pt0, sin(frameCount * this.sway0) * 30);
    this.pt[2] = p5.Vector.add(this.pt2, sin(frameCount * this.sway2) * 30);
    
    push();
    fill('rgba(255, 255, 255, .94)');
    beginShape();
    vertex(this.pt[0].x, this.pt[0].y);
    bezierVertex(this.cp[0].x, this.cp[0].y,
                 this.cp[1].x, this.cp[1].y,
                 this.pt[1].x, this.pt[1].y);
    bezierVertex(this.cp[2].x, this.cp[2].y,
                 this.cp[3].x, this.cp[3].y,
                 this.pt[2].x, this.pt[2].y);
    endShape();

    beginShape();
    curveVertex(this.pt[0].x, this.pt[0].y);
    curveVertex(this.pt[0].x, this.pt[0].y);
    for (let x = this.pt[0].x; x < this.pt[2].x; x++) {
      curveVertex(x, 6 + this.pt[0].y + sin(frameCount * 0.04 + map(x, this.pt[0].x, this.pt[2].x, 0, 4 * PI)) * 6);
    }
    curveVertex(this.pt[2].x, this.pt[2].y);
    curveVertex(this.pt[2].x, this.pt[2].y);
    endShape();
    pop();

    // Eyes and mouth
    push();
    fill(0);
    translate(sin(frameCount*0.05) * 3, 0);
    circle(this.pt[1].x - 20, this.cp[0].y, 20);
    circle(this.pt[1].x + 20, this.cp[3].y, 20);
    ellipse(this.pt[1].x, this.pt[0].y * .4, 12, 2 + noise(frameCount * .03) * 32);
    pop();
    
    if (this.woo != "") {
      push();
      textSize(28);
      blendMode(DIFFERENCE);
      noStroke();
      fill(255);
      text(this.woo, this.pt[1].x + 20, this.pt[0].y * 0.6);
      if ((frameCount % 16) == 0) {
        if (this.woo.length < 12) {
          this.woo += "o";
        } else {
          this.woo = "";
        }
      }
      pop();
    }

    pop();
  }
  
  startWooing() {
     this.woo = "w";
  }
}
