## MditermProject
## [Sketch Link](https://editor.p5js.org/kren2-upbeat/sketches/6Lh7SfTWm)
(
let mic;
let soundP, soundL, soundK;

function preload() {
  soundFormats('wav', 'mp3');
  
  soundP = loadSound('Music/sound1.mp3');
  soundL = loadSound('Music/sound2.mp3');
  soundK = loadSound('Music/sound3.mp3');
}

function setup() {
  createCanvas(400, 400);

  mic = new p5.AudioIn();
  mic.start();

  textSize(20);
  textAlign(CENTER, CENTER);
  fill(255);
}

function draw() {
  background(0);

  let miclevel = mic.getLevel();
  let circleSize = map(miclevel, 0, 1, 20, 400);
  fill(255, 0, 0);
  ellipse(width / 2, height / 2, circleSize, circleSize);

  fill(255);
  text("Press 'P', 'L', or 'K' to play sounds", width / 2, height - 40);

  let playbackRate = map(mouseX, 0, width, 0.5, 2.0);
  soundP.rate(playbackRate);
  soundL.rate(playbackRate);
  soundK.rate(playbackRate);
  
  text('Playback Rate: ' + playbackRate.toFixed(2), width / 2, 30);
}

function keyPressed() {
  console.log("Key pressed:", key);
  
  if (key.toLowerCase() === 'p') {
    playSound(soundP);
	soundL.stop();
	soundK.stop();
  } else if (key.toLowerCase() === 'l') {
    playSound(soundL);
	soundP.stop();
	soundK.stop();
  } else if (key.toLowerCase() === 'k') {
    playSound(soundK);
	soundP.stop();
	soundL.stop();
  } else if (key.toLowerCase() === 's') {
    soundL.stop();
	soundP.stop();
	soundK.stop();
  }
}

function playSound(sound) {
  if (sound.isLoaded()) {
    sound.play();
    console.log("Playing sound:", sound);
  } else {
    console.log("Sound not loaded yet.");
  }
}
)
