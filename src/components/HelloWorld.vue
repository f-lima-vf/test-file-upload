<template>
  <div>
    <v-file-list-input @input="onChange($event)" id="primeiro" accept=".txt, .doc, .docx, .xls, .xlsx, .png, .jpeg, .tiff"></v-file-list-input>
  </div>
  <p>{{ value01 }}</p>
</template>

<script>
import { ref } from 'vue'
import VFileListInput from './FileListInput.vue'

export default {
  name: 'HelloWorld',
  props: {
    accept: {
      type: String,
      default: '.txt, .csv, .md, .doc'
    }
  },
  setup() {
    let value01 = ref([])

    return {
      value01
    }
  },
  components: {
    VFileListInput
  },
  methods: {
    onChange(event) {
      this.value01 = event.target.value
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  body {
    background-color: darkblue;
  }
</style>
