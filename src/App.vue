<script setup>
import { ref} from "vue";
import UserComponent from "@/components/UserComponent.vue";
import SecondsTick from "@/components/secondsTick.vue";
import SearchComponent from "@/components/searchComponent.vue";
const index = ref(0);
const visibleItems = ref(4);


const list = ref([
  {id: 0, name: 'Smith John 0', age: 54, country: 'Morocco'},
  {id: 1, name: 'John Doe 1', age: 50, country: 'Spain'},
  {id: 2, name: 'Jane Doe 2', age: 30, country: 'Senegal'},
  {id: 3, name: 'Smith John 3', age: 54, country: 'Morocco'},
  {id: 4, name: 'John Doe 4', age: 50, country: 'Spain'},
  {id: 5, name: 'Jane Doe 5', age: 30, country: 'Senegal'},
  {id: 6, name: 'Smith John 6', age: 54, country: 'Morocco'},
  {id: 7, name: 'John Doe 7', age: 50, country: 'Spain'},
  {id: 8, name: 'Jane Doe 8', age: 30, country: 'Senegal'},
  {id: 9, name: 'Smith John 9', age: 54, country: 'Morocco'},
  {id: 10, name: 'John Doe 10', age: 50, country: 'Spain'},
  {id: 11, name: 'Jane Doe 11', age: 30, country: 'Senegal'},
]);

</script>
<template>
  <div class="viewport-center">
    <UserComponent :list="list" :index="index || null" :visible-items="visibleItems">
      <template #item="user">
        <img class="avatar" :src="'/placeholder-avatar.jpg'" alt=""/>
        <div>
          <p class="mb-2">{{ user.name }}</p>
          <button>Vote {{ user.votes }}</button>
        </div>
      </template>
    </UserComponent>
    <div class="mb-4 flex flex-wrap items-center justify-center">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        Index:
        <input v-model.number="index" type="number" class="shadow appearance-none border rounded w-6/12 py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" placeholder="0">
      </label>
    </div>
  </div>
  <section class="time-section">
    <SecondsTick/>
  </section>
</template>

<style>
.viewport-center{
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 10px;
  border-bottom: 1px solid ;
}
.time-section{
  display: flex;
  align-items: center;
  justify-content: space-around;
  margin-bottom: 10px;
}
.avatar {
  @apply font-bold object-cover w-24 h-24 rounded-full mr-5 dark:bg-slate-700 bg-slate-200 inline-flex justify-center items-center text-3xl;
}

button {
  @apply bg-blue-600 rounded-md border border-blue-800 px-2  text-white;
}

.pagination {
  @apply flex gap-2 justify-center mt-10;
}

.pagination button {
  @apply bg-blue-600 rounded-md border border-blue-800 p-3 px-6 text-lg text-white;
}

.pagination .active button {
  @apply bg-blue-900;
}
</style>
