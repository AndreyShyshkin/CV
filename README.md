<styles>*, *::before, *::after {
  padding: 0;
  margin: 0 auto;
  box-sizing: border-box;
  transform-style: preserve-3d;
}

$speed: 3s;
$rotateSpeed: 60s;

body {
  background-color: #111;
  color: #fff;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 50px;
  perspective: 800px;
  perspective-origin: center calc(50% - 2.4em);
  overflow: hidden;
}

.cradle {
  position: relative;
  animation: rotate $rotateSpeed infinite linear;
}

@keyframes rotate {
  to { transform: rotateY(360deg); }
}

.floor {
  position: absolute;
  width: 20em;
  height: 20em;
  background-color: #fff;
  background-image:
    radial-gradient(#012a, #111 66%),
    url('https://assets.codepen.io/1948355/marble01.jpg');
  background-size: 20em, 10em;
  transform: translate(-50%, -50%) rotateX(90deg) translateZ(-3em);

  &::after {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 8.5em;
    height: 4.5em;
    background-color: #000;
    filter: blur(0.3em);
  }
}

.wood {
  --width: 0;
  --height: 0;
  --depth: 0;
  $color: #3E2723;

  position: absolute;
  top: 0; left: 0;
  width: var(--width);
  height: var(--height);
  transform: translate(-50%, -50%);

  &.base {
    --width: 8em;
    --height: 1em;
    --depth: 4em;
    transform: translate(-50%, calc(-50% + 2.5em));
  }

  &.poll {
    --width: 0.25em;
    --height: 3em;
    --depth: 0.25em;

    &:nth-child(3) { transform: translate3d(calc(-50% +  3.5em), calc(-50% + 0.5em),  1.5em); }
    &:nth-child(4) { transform: translate3d(calc(-50% +  3.5em), calc(-50% + 0.5em), -1.5em); }
    &:nth-child(5) { transform: translate3d(calc(-50% + -3.5em), calc(-50% + 0.5em),  1.5em); }
    &:nth-child(6) { transform: translate3d(calc(-50% + -3.5em), calc(-50% + 0.5em), -1.5em); }
  }

  &.strecher {
    --width: 8em;
    --height: 0.25em;
    --depth: 1em;

    &:nth-child(7) { transform: translate3d(-50%, calc(-50% - 1em), 1.5em); }
    &:nth-child(8) { transform: translate3d(-50%, calc(-50% - 1em), -1.5em); }

    & .dots::after {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background-image: 
        radial-gradient(circle at 76% 50%, #777 0px, #7770 2px),
        radial-gradient(circle at 63% 50%, #777 0px, #7770 2px),
        radial-gradient(circle at 50% 50%, #777 0px, #7770 2px),
        radial-gradient(circle at 37% 50%, #777 0px, #7770 2px),
        radial-gradient(circle at 24% 50%, #777 0px, #7770 2px),
        ;
    }
  }

  & > * {
    position: absolute;
    box-shadow: 0 0 1em #0007 inset;
    background-size: 5em;
    background-image: url('https://assets.codepen.io/1948355/wood04.png');
  }

  & > .top {
    width: var(--width);
    height: var(--depth);
    transform: translateY(-50%) rotateX(90deg);
    background-color: lighten($color, 15%);
  }

  & > .left {
    width: var(--depth);
    height: var(--height);
    transform: translateX(-50%) rotateY(90deg);
    background-color: lighten($color, 10%);
  }

  & > .right {
    width: var(--depth);
    height: var(--height);
    right: 0;
    transform: translateX(50%) rotateY(90deg);
    background-color: darken($color, 10%);
  }

  & > .front {
    width: var(--width);
    height: var(--height);
    transform: translateZ(calc(var(--depth) / 2));
    background-color: $color;
  }

  & > .back {
    width: var(--width);
    height: var(--height);
    transform: translateZ(calc(var(--depth) / -2));
    background-color: $color;
  }
}

.ballPlate {
  position: absolute;
  top: -1em;
  width: 2em;
  height: 3em;
  transform: translate(-50%, 0%) rotateY(90deg);
  transform-origin: top;

  &:nth-child(9)  {
    left: -2.05em;
    animation: ballPlateStart $speed infinite;
    & .ballWrapper { animation: ballWrapperStart $speed infinite; }
    & .ball { background-position-y: 0%; }
  }
  &:nth-child(10) {
    left: -1.025em;
    animation: ballPlateSwing $speed linear infinite;
    & .ballWrapper { animation: ballWrapperSwing $speed linear infinite; }
    & .ball { background-position-y: 25%; }
  }
  &:nth-child(11) {
    left: 0;
    animation: ballPlateSwing $speed linear infinite;
    & .ballWrapper { animation: ballWrapperSwing $speed linear infinite; }
    & .ball { background-position-y: 50%; }
  }
  &:nth-child(12) {
    left: 1.025em;
    animation: ballPlateSwing $speed linear infinite;
    & .ballWrapper { animation: ballWrapperSwing $speed linear infinite; }
    & .ball { background-position-y: 75%; }
  }
  &:nth-child(13) {
    left: 2.05em;
    animation: ballPlateEnd $speed infinite;
    & .ballWrapper { animation: ballWrapperEnd $speed infinite; }
    & .ball { background-position-y: 100%; }
  }

  @keyframes ballPlateSwing {
    0%, 100% { transform: translate(-50%, 0%) rotateY(90deg) rotateX(5deg); }
    50% { transform: translate(-50%, 0%) rotateY(90deg) rotateX(-5deg); }
  }

  @keyframes ballPlateStart {
    0%, 100% {
      animation-timing-function: ease-out;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(5deg);
    }
    50% {
      animation-timing-function: ease-out;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(-5deg);
    }
    75% {
      animation-timing-function: ease-in;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(-80deg);
    }
  }

  @keyframes ballPlateEnd {
    0%, 100% {
      animation-timing-function: ease-out;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(5deg);
    }
    25% {
      animation-timing-function: ease-in;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(80deg);
    }
    50% {
      animation-timing-function: ease-out;
      transform: translate(-50%, 0%) rotateY(90deg) rotateX(-5deg);
    }
  }

  @keyframes ballWrapperSwing {
    0%, 100% { transform: rotateY(90deg) rotate(-5deg); }
    50% { transform: rotateY(90deg) rotate(5deg); }
  }

  @keyframes ballWrapperStart {
    0%, 100% {
      animation-timing-function: ease-out;
      transform: rotateY(90deg) rotate(-5deg);
    }
    50% {
      animation-timing-function: ease-out;
      transform: rotateY(90deg) rotate(5deg);
    }
    75% {
      animation-timing-function: ease-in;
      transform: rotateY(90deg) rotate(80deg);
    }
  }

  @keyframes ballWrapperEnd {
    0%, 100% {
      animation-timing-function: ease-out;
      transform: rotateY(90deg) rotate(-5deg);
    }
    25% {
      animation-timing-function: ease-in;
      transform: rotateY(90deg) rotate(-80deg);
    }
    50% {
      animation-timing-function: ease-out;
      transform: rotateY(90deg) rotate(5deg);
    }
  }

  .ballWrapper {
    position: absolute;
    bottom: 0.1em; left: calc(50% - 0.5em);
    width: 1em;
    height: 1em;
  }

  .ball {
    position: absolute;
    width: 1em;
    height: 1em;
    background-color: #fff;
    border-radius: 50%;
    background-image:
      radial-gradient(circle at top, #fff, #678a, #000),
      url('https://assets.codepen.io/1948355/marble01.jpg'),
      ;
    background-size: 1em, 5em;
    box-shadow: 0 0 10px #000a inset;
    animation:
      backPos $rotateSpeed * 2 infinite linear,
      rotate $rotateSpeed infinite linear reverse;

    @keyframes backPos {
      from { background-position-x: center, 5em;}
      to { background-position-x: center, 0;}
    }
  }

  .line {
    position: absolute;
    top: 0;
    width: 2px; height: 2.15em;
    background-color: #fff7;
    transform-origin: top;
    &::after {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background-color: #fff7;
      transform: rotateY(90deg);
    }

    &:nth-child(2) { transform: translateX(-1px) rotate(-20deg); }
    &:nth-child(3) { right: 0; transform: translateX(1px) rotate(20deg); }
  }
}

.shadow {
  position: absolute;
  top: 50%;
  width: 3em;
  height: 3em;
  background-image: radial-gradient(#0006, #0000 50%);

  &:nth-child(1) {
    animation:
      shadowSwing $speed ease-out infinite,
      shadowStart $speed ease-out infinite;
  }
  &:nth-child(2) {
    left: 2.975em;
    animation: shadowSwing $speed linear infinite;
  }
  &:nth-child(3) {
    left: 4em;
    animation: shadowSwing $speed linear infinite;
  }
  &:nth-child(4) {
    left: 5.025em;
    animation: shadowSwing $speed linear infinite;
  }
  &:nth-child(5) {
    animation:
      shadowSwing $speed ease-out infinite,
      shadowEnd $speed ease-out infinite;
  }

  @keyframes shadowSwing {
    0%, 100% { transform: translate(-50%, -50%) rotateX(0deg) translateZ(-0em) translateX(10px); }
    50% { transform: translate(-50%, -50%) rotateX(0deg) translateZ(-0em) translateX(-10px); }
  }

  @keyframes shadowStart {
    0%, 50%, 100% { left: 1.95em; opacity: 1; }
    75% {
      left: 0; opacity: -0.5;
      animation-timing-function: ease-in;
    }
  }

  @keyframes shadowEnd {
    0%, 50%, 100% { left: 6.05em; opacity: 1; }
    25% {
      left: 8em; opacity: -0.5;
      animation-timing-function: ease-in;
    }
  }
}

.twitterLink {
  font-size: 24px;
}</styles>
<div class="cradle">

  <div class="floor"></div>

  <div class="wood base">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back"></div>
    <div class="top">
      <div class="shadow"></div>
      <div class="shadow"></div>
      <div class="shadow"></div>
      <div class="shadow"></div>
      <div class="shadow"></div>
    </div>
  </div>
  <div class="wood poll">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back"></div>
  </div>
  <div class="wood poll">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back"></div>
  </div>
  <div class="wood poll">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back"></div>
  </div>
  <div class="wood poll">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back"></div>
  </div>
  <div class="wood strecher">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front dots"></div>
    <div class="back"></div>
    <div class="top"></div>
  </div>
  <div class="wood strecher">
    <div class="left"></div>
    <div class="right"></div>
    <div class="front"></div>
    <div class="back dots"></div>
    <div class="top"></div>
  </div>

  <div class="ballPlate">
    <div class="ballWrapper">
      <div class="ball"></div>
    </div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
  <div class="ballPlate">
    <div class="ballWrapper">
      <div class="ball"></div>
    </div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
  <div class="ballPlate">
    <div class="ballWrapper">
      <div class="ball"></div>
    </div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
  <div class="ballPlate">
    <div class="ballWrapper">
      <div class="ball"></div>
    </div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
  <div class="ballPlate">
    <div class="ballWrapper">
      <div class="ball"></div>
    </div>
    <div class="line"></div>
    <div class="line"></div>
  </div>
</div>
