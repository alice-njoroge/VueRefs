<script setup>
import {computed, onMounted, ref} from "vue";

const currSecond = ref(new Date().getSeconds());
let interval;

const updateSeconds = () => {
  currSecond.value = new Date().getSeconds();
}
onMounted(() => {
  interval = setInterval(updateSeconds, 1000)
});
clearInterval(interval)

// import { useNow } from "@vueuse/core"
// const now = useNow();
//
// const currSecond = computed(()=>{
//   return now.value.getSeconds()
// })


</script>

<template>
  <div class="seconds-card relative">
    <Transition appear>
      <span class="seconds absolute" :key="currSecond"> {{ currSecond }}</span>
    </Transition>
  </div>
</template>

<style scoped>
.seconds-card {
  box-shadow: 0 0 4px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 30px;
  width: 20%;
  min-height: 100px;
}

.seconds {
  font-style: italic;
  font-weight: bold;
}

.v-enter-active,
.v-leave-active {
  transition: all .5s ease;
}

.v-enter-from{
  transform: translateY(-10px);
}
.v-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
.v-leave-active{
  position: absolute;
}



</style>