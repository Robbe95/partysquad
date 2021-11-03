<script setup>
let container = null
let text = null

onMounted(() => {
  text = document.querySelector('h1')
  container = document.querySelector('.container')
  container.addEventListener('mousemove', shadow)
})

function shadow(e) {
  const { offsetWidth: width, offsetHeight: height } = container
  let { offsetX: x, offsetY: y } = e
  if (this !== e.target) {
    x = x + e.target.offsetLeft
    y = y + e.target.offsetTop
  }
  const movement = 100
  const xMovement = (x / width) * movement - movement / 1.2
  const yMovement = (y / width) * movement - movement / 1.2
  text.style.textShadow = `  
    ${xMovement}px ${yMovement}px 0 rgba(218, 83, 44, 0.7),
    ${xMovement * -1}px ${yMovement}px 0 rgba(45, 137, 239, 0.6),
    ${xMovement}px ${yMovement * -1}px 0 rgba(96, 60, 186, 0.5),
    ${xMovement * -1}px ${yMovement * -1}px 0 rgba(0, 163, 0, 0.4)`
  // add as many shadows as you like 🙂
}

</script>

<template>
  <div class="min-h-screen min-w-screen background flex items-center justify-center overflow-hidden container">
    <div>
      <h1 class="2xl:text-15xl lg:text-10xl text-5xl text-red-500 text-animation mb-20">
        PARTYSQUAD
      </h1>
      <div class="text-white text-center">
        Coming soon...
      </div>
    </div>
  </div>
</template>

<style scoped>
.background {
  background: linear-gradient(110deg, #fdcd3b 60%, black 60%);

}

.text-animation {
  animation: textanimation 3s infinite;
  font-family: "Comic Sans MS", "Comic Sans", cursive;
}

@keyframes textanimation
{
  0%   {transform: rotate(20deg) scale(1);}
  16%  {transform: rotate(20deg) scale(1.2);}
  33%  {transform: rotate(20deg) scale(1);}
  50% {transform: rotate(-20deg) scale(1);}
  67% {transform: rotate(-20deg) scale(1.2);}
  83% {transform: rotate(-20deg) scale(1);}
  100% {transform: rotate(20deg) scale(1);}

}

</style>

<route lang="yaml">
meta:
  layout: home
</route>
