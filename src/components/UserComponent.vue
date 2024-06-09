<script setup>
import {computed, onMounted, ref, watch} from "vue";
const itemRefs = ref([]);
const itemHeight = ref(0);

const props = defineProps({
  list: { type: Array, default: ()=>[]},
  visibleItems: {default: 4, type: Number},
  index: {default: 0, type: Number}
});
onMounted(()=>{
  if (itemRefs.value){
    itemHeight.value = itemRefs.value[0].clientHeight
  }
});


const computedHeight = computed(()=>{
  return itemHeight.value * props.visibleItems
})
</script>
<template>
  <div
      class="root-card m-5 w-6/12 mx-auto border border-black overflow-hidden"
      :style="`height: ${computedHeight}px`"
  >
    <TransitionGroup name="list" tag="ul" class="user-wrapper">
      <li
          ref="itemRefs"
          class="user-card"
          v-for="(user, index) in list.slice(props.index)"
          :key="user.id"
          :tabindex="index + 1"
      >
       <slot name="item" v-bind="user"> </slot>
      </li>
    </TransitionGroup>
  </div>
</template>
<style scoped>
.list-move, /* apply transition to moving elements */
.list-enter-active{
  transition: all 0.5s ease-out 0.25s;
}
.list-leave-active {
  transition: all 0.5s ease-in;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
  position: absolute;
}

</style>