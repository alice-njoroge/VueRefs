<script setup>
import {computed, onMounted, ref, watch} from "vue";

const itemRefs = ref([]);
const itemHeight = ref(0);

const props = defineProps({
  list: {type: Array, default: () => []},
  visibleItems: {type: Number},
  index: {default: 0, type: [Number]}
});
onMounted(() => {
  if (itemRefs.value) {
    itemHeight.value = itemRefs.value[0].clientHeight
  }
});

watch(
    () => props.index,
    (newVal) => {
      if (newVal !== null && newVal < props.list.length){
        itemRefs.value[newVal].scrollIntoView({ behavior: 'smooth' }); //ref.scrollIntoView({behavior})
      } else{
        itemRefs.value[0].scrollIntoView({ behavior: 'smooth' });
      }
    }
)


const computedHeight = computed(() => {
  return itemHeight.value * props.visibleItems;
})
</script>
<template>
  <div
      class="root-card"
      :style="`height: ${computedHeight}px`"
      v-if="list.length"
  >
    <ul>
      <li
          ref="itemRefs"
          class="user-card"
          v-for="(user, index) in list"
          :key="user.id"
          :tabindex="index + 1"
      >
        <slot name="item" v-bind="user"></slot>
      </li>
    </ul>
  </div>
</template>
<style scoped>
.root-card {
  @apply flex flex-wrap justify-center items-center m-5 w-6/12 mx-auto border border-black overflow-hidden;
}

.user-wrapper {
  @apply gap-10 justify-center ;
}

.user-card {
  @apply p-3 shadow-lg rounded w-80 flex items-center;
}

</style>