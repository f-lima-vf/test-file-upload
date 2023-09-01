<template>
  <div>
    <VFileListInput @input="onChange" id="primeiro" accept="accept" v-model="value01">
    </VFileListInput>
  </div>
  <p>HelloWorld</p>
  <ul class="file-list">
      <li v-for="(file, index) in value01" :key="index">
          <span>{{ file.name }}</span>
      </li>
  </ul>
</template>

<style>
  body {
    background-color: whitesmoke;
  }
</style>

<script>
import { ref } from 'vue'
import VFileListInput from './FileListInput.vue'

export default {
  name: 'HelloWorld',
  setup() {
    const accept = ref('.txt, .csv, .md, .doc')
    const value01 = ref([]);

    function onChange(newValue) {
      value01.value = newValue;
    }

    return {
      accept,
      value01,
      onChange,
    };
  },
  components: {
    VFileListInput,
  },
};
</script>
