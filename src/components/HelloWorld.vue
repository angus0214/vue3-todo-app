<script setup>
import { ref } from 'vue';

defineProps({
  msg: String,
});

const count = ref(0);
const title = 'title is me';
const htmlText = `<span>This is html</span>`;
const className = 'test-class';
const testAttr = {
  class: 'test-class',
  id: 'test-text',
};
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count+=3">count is {{ count }}</button>
    <p>
      {{ title }}
    </p>
    <div v-text="title"></div>
    <div>reverse:{{ title.split('').reverse().join('') }}</div>
    <div v-html="htmlText"></div>
    <div :class="className">Hey Class</div>
    <div :class="`${className}-blue`">Hey Class</div>
    <div v-bind="testAttr">V-bind Obeject</div>
    <div>
      <div v-if="count < 18">未成年</div>
      <div v-else-if="(count === 18)">剛好成年</div>
      <div v-else>妳已經是大人了</div>
    </div>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
.test-class {
  color: red;
}
.test-class-blue {
  color: blue;
}
#test-text {
  font-size: 2rem;
}
</style>
