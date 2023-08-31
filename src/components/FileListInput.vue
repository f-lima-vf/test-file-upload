<template>
    <div v-bind:id="this.id">
        <input class="file-input" type="file" multiple v-bind:disabled="disabled" v-bind:accept="accept" v-on:change="onChange">
        <div>
            <ul class="file-list">
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
    import UploadFileList from './UploadFileList.vue';
    
    export default defineComponent({
        props: {
            id: {
                type: String,
                required: true
            },
            accept: String
        },
        setup() {
            let fileList = ref([]);

            fileList = [];

            return {
                fileList
            }
        },
        data: function () {
            return {
                files: new UploadFileList()
            }
        },
        methods: {
            add(file) {
                this.fileList.push(file);
                this.renderList();
            },
            remove(fileIndex) {
                this.fileList = this.fileList.filter((el) => el.index != fileIndex);
                this.renderList();
            },
            renderList() {
                let fileListElement = document.getElementById(this.id).children[1].children[0];
                fileListElement.innerHTML = '';
                let index = 0; 
                this.fileList.forEach(file => {
                    file.index = index++;
                    fileListElement.innerHTML += `<li><label class="mdi-paperclip" onclick="window.dispatchEvent(new CustomEvent('remove', { detail: { item: ${ file.index } } }))">X</label><a href="${ file.url }" target="_blank">${ file.name }</a></li>`;
                });
            },
            onChange(e) {
                e.preventDefault();
                for (let el of e.target.files) {
                    let file = new UploadFile(el);
                    this.add(file);
                }
                let fs = new UploadFileList();
                for(let f of this.fileList) {
                    fs.list.push(f.file);
                }
                this.files = fs;
                //this.processFiles(e.target.files);
                return this.modelValue
            },
            onRemove(e) {
                this.remove(e.detail.item);
            }
        },
        mounted() {
            window.addEventListener('remove', this.onRemove);
            return true;
        },
    })
</script>
