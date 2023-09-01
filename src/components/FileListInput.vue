<template>
    <div v-bind:id="id">
        <input class="file-input" type="file" multiple v-bind:disabled="disabled" v-bind:accept="accept" @input="onChange($event)">
        <div>
            <ul class="file-list">
                <li v-for="(file, index) in fileList" :key="index">
                    <label class="mdi-paperclip" @click="remove(index)">X</label>
                    <a :href="file.url" target="_blank">{{ file.name }}</a>
                </li>
            </ul>
        </div>
    </div>
</template>

<style>
    .file-list label { 
        padding: 2mm;
    }
    .file-list li {
        list-style-type: none;
    }
</style>

<script>
    import { defineComponent, ref  } from 'vue'
    import UploadFile from './UploadFile.vue';
    import axios from 'axios';
    
    export default defineComponent({
        props: {
            id: {
                type: String,
                required: true
            },
            accept: String
        },
        emits: ["input", "update:modelValue"],
        setup(props, { emit }) {
            emit('input');
            emit('update:modelValue');
            let fileList = ref([]);

            fileList = [];

            return {
                fileList
            }
        },
        data: function () {
            return {
                files: ref([])
            }
        },
        methods: {
            add(file) {
                this.fileList.push(file);
            },
            remove(fileIndex) {
                this.fileList = this.fileList.filter((el) => el.index != fileIndex);
            },
            onChange(e) {
                for (let el of e.target.files) {
                    let file = UploadFile(el);
                    this.add(file);
                }
                let fs = [];
                for(let f of this.fileList) {
                    fs.list.push(f.file);
                }
                this.files.values = fs;
                this.modelValue = fs;
                //this.processFiles(e.target.files);
                e.preventDefault();
            },
            async uploadFiles() {
                for (let file of this.files) {
                    const formData = new FormData();
                    formData.append('file', file);
                    try {
                        const response = await axios.post('/upload', formData);
                        // Handle success here
                        console.log(response);
                    } catch (error) {
                        // Handle error here
                        console.error(error);
                    }
                }
            }
        },
        mounted() {
            //window.addEventListener('remove', this.onRemove);
            return true;
        },
    })
</script>
