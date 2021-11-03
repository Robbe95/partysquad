<script setup lang="ts">
</script>

<template>
  <div class="min-h-screen min-w-screen background flex items-center justify-center">
    <div>
      <div class="text-20xl text-red-500 text-animation mb-20">
        PARTYSQUAD
      </div>
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
