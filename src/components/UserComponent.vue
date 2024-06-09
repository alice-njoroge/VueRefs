<script setup>
import {computed, onMounted, ref} from "vue";
const itemRefs = ref([]);
const itemHeight = ref(0);

const props = defineProps({
  totalNumberOfPages: {default: 3, type: Number},
  currentPage: { default: 1, type: Number},
  list: { type: Array, default: ()=>[]},
  visibleItems: {default: 4, type: Number}
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
    <ul class="user-wrapper">
      <li
          ref="itemRefs"
          class="user-card"
          v-for="(user, index) in list"
          :key="user.id"
          :tabindex="index + 1"
      >
       <slot name="item" v-bind="user"> </slot>
      </li>
    </ul>
  </div>
  <div>
    <ul class="pagination">
      <li
          v-for="n in totalNumberOfPages"
          :key="n"
      >
        <button>{{ n }}</button>
      </li>
    </ul>
  </div>
</template>
<style scoped>

</style>