<script setup>
const amount = ref(50)
const container = ref()
onMounted(() => {
  container.value.addEventListener('mousemove', move)
})
const xMovement = ref(0)
const yMovement = ref(0)

function move(e) {
  let x = e.x
  let y = e.y
  x = x - (container.value.getBoundingClientRect().width / 2)
  y = y - (container.value.getBoundingClientRect().height / 2)
  const movement = 100
  xMovement.value = (x / container.value.getBoundingClientRect().width)
  yMovement.value = (y / container.value.getBoundingClientRect().height)
}

</script>

<template>
  <div ref="container" class="bg-black h-screen w-screen flex items-center justify-center">
    <div class=" flex items-center justify-center overflow-hidden h-full w-full relative">
      <div v-for="i in amount" :key="i" class="absolute">
        <div
          class="bg-transparent border-5px border-white rounded-full transition duration-75 overflow-hidden"
          :style="`height: ${i * 50 }px;width: ${i * 50 }px; transform: translateX(${xMovement * i * 1}px) translateY(${yMovement * i * 1}px);`"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>

<route lang="yaml">
meta:
  layout: home
</route>
