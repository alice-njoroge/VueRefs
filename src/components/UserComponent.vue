<script setup>
const props = defineProps({
  total: {default: 3, type: Number},
  current: { default: 1, type: Number},
  list: { type: Array, default: ()=>[]}
})
</script>
<template>
  <div class="root-card m-5 w-6/12 mx-auto border border-black h-80 overflow-hidden" >
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
          v-for="n in total"
          :key="n"
      >
        <button>{{ n }}</button>
      </li>
    </ul>
  </div>
</template>
<style scoped>

</style>