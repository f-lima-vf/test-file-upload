<template>
  <div>
    <VFileListInput @input="onChange" id="primeiro" accept=".txt, .csv, .md, .doc, .docx" v-model="value01">
    </VFileListInput>
  </div>
  <p>Lista de arquivos a subir:</p>
  <ul class="file-list">
      <li v-for="(file, index) in value01" :key="index">
          <span>{{ file.name }} ({{ file.size }})</span>
      </li>
  </ul>
</template>

<style>
  body {
    background-color: whitesmoke;
  }

  #app {
    text-align: left !important;
  }
</style>

<script>
import { ref } from 'vue'
import VFileListInput from './file-input/FileListInput.vue'

export default {
  name: 'HelloWorld',
  setup() {
    const accept = ref('.txt, .csv, .md, .doc, *.docx')
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
