<script setup>
import { reactive, ref } from 'vue';
const data = reactive([]);
const inputTask = ref('');
const inputEdit = ref('');
const createTask = () => {
  let tempData = {
    title: inputTask.value,
    checked: false,
  };
  data.push(tempData);
  inputTask.value = '';
};
const finishTask = (index) => {
  data[index].checked = !data[index].checked;
};
const deleteTask = (index) => {
  data.splice(index, 1);
};
const btnEditTask = (index) => {
  inputEdit.value = data[index].title;
  data[index].isEditing = true;
};
const editTask = (index) => {
  data[index].title = inputEdit.value;
  data[index].isEditing = false;
};
const clearAllTask = () => {
  data.splice(0);
};
</script>

<template>
  <div class="w-full h-screen bg-gray-700 pt-8">
    <div class="bg-gray-100 p-3 max-w-md mx-auto">
      <div class="text-center">
        <h1 class="text-3xl font-bold">Vue3 Todo App</h1>
        <div class="mt-6 flex">
          <input
            class="w-80 border-b-2 border-gray-500 text-black p-3"
            type="text"
            placeholder="輸入待辦事項"
            v-model="inputTask"
          />
          <button
            class="ml-2 border-2 bg-green-500 text-white p-3 font-bold hover:bg-green-600 rounded-lg flex"
            @click="createTask"
          >
            Add
          </button>
        </div>
      </div>
      <div class="mt-8">
        <div
          class="text-center font-bold text-2xl text-gray-700"
          v-if="data.length === 0"
        >
          趕快新增待辦事項吧 !
        </div>
        <ul v-else>
          <li class="p-2 rounded-lg" v-for="(item, index) in data" :key="index">
            <div class="flex align-middle flex-row justify-between">
              <div class="p-2">
                <input
                  type="text"
                  class="px-1 border-2 border-blue-500 focus:outline-none focus:border-blue-500"
                  v-if="item.isEditing"
                  v-model="inputEdit"
                  @keyup.enter="editTask(index)"
                />
                <p
                  v-else
                  class="text-lg font-bold"
                  :class="{
                    'line-through': item.checked,
                    'text-gray-400': item.checked,
                  }"
                >
                  {{ item.title }}
                </p>
              </div>
              <div class="flex">
                <button
                  v-if="!item.checked"
                  class="border-2 bg-green-400 text-white p-2 font-bold hover:bg-green-500 rounded-lg flex"
                  @click="finishTask(index)"
                >
                  Finish
                </button>
                <button
                  v-else
                  class="border-2 bg-yellow-400 text-white p-2 font-bold hover:bg-yellow-500 rounded-lg flex"
                  @click="finishTask(index)"
                >
                  Redo
                </button>
                <button
                  class="ml-2 border-2 bg-blue-400 text-white p-2 font-bold hover:bg-blue-500 rounded-lg flex"
                  @click="btnEditTask(index)"
                >
                  Edit
                </button>
                <button
                  class="flex text-red-500 p-2 rounded-lg"
                  @click="deleteTask(index)"
                >
                  <svg
                    class="h-6 w-6 text-red-500 hover:text-red-700"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  >
                    <circle cx="12" cy="12" r="10" />
                    <line x1="15" y1="9" x2="9" y2="15" />
                    <line x1="9" y1="9" x2="15" y2="15" />
                  </svg>
                </button>
              </div>
            </div>
            <hr class="mt-2" />
          </li>
        </ul>
      </div>
      <div class="mt-8">
        <button
          class="border-2 font-bold border-red-500 p-2 text-red-500 hover:bg-red-600 hover:text-white rounded-lg"
          @click="clearAllTask"
        >
          Clear All Task
        </button>
      </div>
    </div>
  </div>
</template>

<style></style>
