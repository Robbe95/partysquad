<script setup>
import gsap from 'gsap'
import { MotionPathPlugin } from 'gsap/dist/MotionPathPlugin'

gsap.registerPlugin(MotionPathPlugin)

const isPoopPage = ref(Math.random() > 0.5)

const removePoop = () => {
  const poopTimeline = gsap.timeline()
  poopTimeline.to('#poop', {
    motionPath: {
      path: [{ x: 0, y: 0 }, { x: 100, y: 90 }, { x: 170, y: 150 }, { y: 600, x: 170 }],
      type: 'cubic',
    },
    ease: 'none',
    duration: 1.2,
  })
    .to('#poop', { rotate: 250, duration: 1.2, ease: 'none', delay: -1.2 })
    .to('#poop', { display: 'none' })
    .to('#maarten', { y: '100%' })
    .to('#unicorn-wings', { y: '20%', duration: 5 })
    .to('#glow', { opacity: 0.7, duration: 2, delay: -5 })
    .to('#glow', { opacity: 0, duration: 1, delay: 1 })
    .to('#unicorn', {
      '--shadow-color2': 'rgba(228, 195, 41, 0.8)',
      '--shadow-blur2': '40px',
      'duration': 2,
      'delay': -5,
    })
    .to('#unicorn', {
      '--shadow-color2': 'transparent',
      '--shadow-blur2': '0',
      'duration': 1,
    })

  // const poopTimeline = gsap.timeline()

  // poopTimeline
  //   .to('#poop', { x: 40, duration: 0.2, ease: 'none' })
  //   .to('#poop', { y: 100, x: 90, duration: 0.2, ease: 'none' })
  //   .to('#poop', { x: 170, y: 150, duration: 0.3, ease: 'none' })
  //   .to('#poop', { y: 400, duration: 0.5 })
}

const setPositions = () => {
  gsap.set('#unicorn-wings', { y: '100%' })
  gsap.set('#joren', { x: '-100%' })
  gsap.set('#bierjoren', { y: '150%' })

  gsap.set('#ellen', { x: '-40vw', y: '-40vh' })
  gsap.set('#poop', { y: '-80px', opacity: 0 })
  gsap.set('.bubble', { y: '200%', x: '200%', opacity: 0 })
}

const jorenGetsBeer = () => {
  const beerTimeline = gsap.timeline()
  beerTimeline
    .to('#joren', { x: '-100%' })
    .to('#bierjoren', { y: '25%', duration: 1, delay: 2 })
}

const jorenAnimation = () => {
  const jorenTimeline = gsap.timeline()
  jorenTimeline
    .to('#joren', { x: 0, duration: 1, delay: 3 })
    .to('.bubble', { x: 0, y: 0, rotate: 90, opacity: 1, duration: 1, delay: 0.5 })
    .to('.bubble', { opacity: 0, duration: 1, delay: 1 })
}

const ellenAnimation = () => {
  const ellenTimeline = gsap.timeline()
  ellenTimeline
    .to('#ellen', { x: '40vw', y: '20vh', duration: 1 })
    .to('#ellen', { rotateY: 180, duration: 0.5 })
    .to('#ellen', { x: '-17vw', y: '25vh', duration: 1 })
    .to('#poop', { y: 0, opacity: 1, duration: 0.5 })

  // POOP VIBRATION
    .to('#ellen', { rotate: -1, duration: 0.1, delay: -0.5 })
    .to('#ellen', { rotate: 1, duration: 0.1, delay: -0.45 })
    .to('#ellen', { rotate: -1, duration: 0.1, delay: -0.40 })
    .to('#ellen', { rotate: 1, duration: 0.1, delay: -0.35 })
    .to('#ellen', { rotate: -1, duration: 0.1, delay: -0.30 })
    .to('#ellen', { rotate: 1, duration: 0.1, delay: -0.25 })
    .to('#ellen', { rotate: -1, duration: 0.1, delay: -0.20 })
    .to('#ellen', { rotate: 1, duration: 0.1, delay: -0.15 })
    .to('#ellen', { rotate: -1, duration: 0.1, delay: -0.10 })
    .to('#ellen', { rotate: 1, duration: 0.1, delay: -0.05 })
    .to('#ellen', { rotate: -0, duration: 0.1, delay: 0 })

    .to('#ellen', { rotateY: 0, duration: 0.5 })
    .to('#ellen', { x: 0, y: 0, duration: 1 })
}

const moveEllen = () => {
  const moveEllenTimeline = gsap.timeline()
  moveEllenTimeline
    .to('#ellen', {
      x: 1500,
      y: 1000,
      duration: 2,
    },
    )
}

const objectsAnimation = () => {
  let objects = ['#star1', '#star2', '#star3', '#star4', '#star5', '#star6', '#banana', '#fish']
  objects = objects
    .map(value => ({ value, sort: Math.random() }))
    .sort((a, b) => a.sort - b.sort)
    .map(({ value }) => value)
  objects.forEach((element, index) => {
    gsap.from(element, { scale: 0, ease: 'elastic', duration: 1, delay: index * 0.4 + 3 })
  })
}

const titleAnimation = () => {
  gsap.from('#title', { scale: 0, ease: 'elastic', duration: 3, delay: 4 })
}

const setupAnimations = () => {
  setPositions()
  jorenAnimation()
  ellenAnimation()
  objectsAnimation()
  titleAnimation()
}

const randomOrbit = (element, movement) => {
  gsap.to(element, {
    svgOrigin: '10 10',
    rotate: 360,
    repeat: -1,
    ease: 'none',
    duration: 2,
  })
}

const setupOrbit = () => {
  const minMovement = 200
  const maxMovement = Math.min(window.innerWidth, window.innerHeight)
  randomOrbit('#orbit', Math.floor(Math.random() * (400 - 200 + 1) + 0))
}

const loading = ref(true)
onMounted(() => {
  setTimeout(() => {
    loading.value = false

    setupAnimations()
  }, 2000)

  // setupOrbit()
})
</script>

<template>
  <div class="relative">
    <transition name="fade">
      <div v-if="loading" class="w-screen h-screen absolute top-0 left-0 z-50">
        <div class="loading w-full h-full flex items-center justify-center">
          <div class="text-3xl text-white">
            Loading...
          </div>
        </div>
      </div>
    </transition>

    <div ref="container" class="bg-black h-screen min-w-screen relative overflow-hidden flex items-center justify-center">
      <div class="flex items-center justify-center w-full h-full absolute" target="0">
        <img id="title" class="z-20" src="@/assets/title.png" />
      </div>

      <img class="absolute w-full h-full object-cover" src="@/assets/background.png" />
      <img
        v-for="i in 20"
        :id="'cow-' +i"
        :key="i"
        class="absolute z-0 cow w-auto -top-2/8 right-0 scale-50"
        target="0"
        src="@/assets/cow.png"
      />

      <!-- <div id="orbit" class="orbit z-0 h-80 w-80 mt-80 ml-80">
      <img class="transform z-" src="@/assets/maarten.png" />
    </div> -->
      <div id="unicorn-wings" class="absolute bottom-0 left-30 z-20">
        <div class="relative rotate-y-180 transform">
          <img id="unicorn" class="h-180" src="@/assets/unicorn.png" />
          <img id="wings" class="absolute -top-20 -left-12 -z-10 h-120" src="@/assets/wings.png" />
          <img id="glow" class="absolute top-5 left-24 -z-10 h-40 opacity-40 opacity-0" src="@/assets/glow.png" />
        </div>
      </div>

      <div class="absolute bottom-0 left-40">
        <img id="maarten" class="" src="@/assets/maarten.png" />
        <div class="hover:scale-110 transform transition absolute -top-14 left-10 cursor-pointer" @click="removePoop">
          <img id="poop" class="h-30" src="@/assets/poop.png" />
        </div>
      </div>
      <img id="robbe" class="absolute bottom-0 left-0" src="@/assets/robbe.png" />
      <div class="absolute bottom-1/2 left-0 z-10">
        <div class="transform hover:scale-110 transition" target="1">
          <img id="joren" src="@/assets/joren.png" class="cursor-pointer" @click="jorenGetsBeer" />
        </div>
        <div class="absolute left-10 -bottom-10">
          <div
            class="bubble bubble-bottom-left "
          >
            Zal ik wa pintjes halen?
          </div>
        </div>
      </div>
      <div class="absolute bottom-1/2 -left-0 h-80 rotate-90 transform">
        <img id="bierjoren" class="h-full" src="@/assets/bierjoren.png" />
      </div>
      <img id="fish" class="absolute bottom-1/8 left-1/2" src="@/assets/fish.png" />

      <div class="absolute bottom-1/2 left-1/4 hover:scale-110 transition transform cursor-pointer">
        <img id="ellen" class=" " src="@/assets/ellen.png" @click="moveEllen" />
      </div>
      <img id="sm" class="absolute bottom-0 right-25 z-10" src="@/assets/sm.png" />
      <div class="absolute bottom-40 right-20 z-0">
        <div class="relative">
          <img id="leander" class="" src="@/assets/leander.png" />
          <img id="banana" class="absolute -left-24 top-40 -z-10" src="@/assets/banana.png" />
        </div>
        <img class="h-8 transform rotate-y-180 absolute top-17 right-28" src="@/assets/tongue.gif" />
      </div>
      <div>
        <img id="star1" class="absolute top-1/6 left-5/12" src="@/assets/star.svg" />
        <img id="star2" class="absolute top-7/12 left-1/12 transform rotate-54" src="@/assets/star.svg" />
        <img id="star3" class="absolute top-10/12 left-4/12 transform rotate-34" src="@/assets/star.svg" />
        <img id="star4" class="absolute top-11/12 left-6/12 transform rotate-170" src="@/assets/star.svg" />
        <img id="star5" class="absolute top-6/12 left-8/12 transform rotate-120" src="@/assets/star.svg" />
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">

.body {
  background-color: purple;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter-from, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.loading {
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradient 15s ease infinite;
}

@keyframes gradient {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}

@for $i from 1 through 20 {
  #cow-#{$i} {
    animation: cow-animation 2s 1 normal forwards;
    animation-delay: 20ms * $i + 2s;
    opacity: 0;
  }
}

#cow-1 {
  filter: drop-shadow(0 25px 25px rgba(0, 0, 0, 0.5));
}

@keyframes cow-animation {
  from   {transform: rotate(0deg) scale(0); opacity: 0;}
  to {transform: rotate(360deg) scale(0.5); opacity: 1;}
}

.bubble {
  position: relative;
  font-family: sans-serif;
  font-size: 18px;
  line-height: 24px;
  width: 300px;
  background: #fff;
  border-radius: 40px;
  padding: 24px;
  text-align: center;
  color: #000;
}

.bubble-bottom-left:before {
  content: "";
  width: 0px;
  height: 0px;
  position: absolute;
  border-left: 24px solid #fff;
  border-right: 12px solid transparent;
  border-top: 12px solid #fff;
  border-bottom: 20px solid transparent;
  left: 32px;
  bottom: -24px;
}

#unicorn {
  --shadow-blur: 20px;
  --shadow-blur2: 20px;

  --shadow-color: transparent;
  --shadow-color2: transparent;
  -webkit-filter: drop-shadow(20px 20px var(--shadow-blur) var(--shadow-color)) drop-shadow(2px 2px var(--shadow-blur2) var(--shadow-color2));
  filter: drop-shadow(20px 20px var(--shadow-blur) var(--shadow-color)) drop-shadow(2px 2px var(--shadow-blur2) var(--shadow-color2));
}
</style>

<route lang="yaml">
meta:
  layout: home
</route>
