<template>
    <div v-bind:id="id" class="class">
        <button @click="selectFiles">{{ label }}</button>
        <input class="file-input" type="file" multiple v-bind:disabled="disabled" 
            v-bind:accept="accept" @input="onChange($event)" title="Selecione">
        <div>
            <label v-if="fileList.length > 0">{{ title }}</label>
            <ul class="file-list">
                <li v-for="(file, index) in fileList" :key="index">
                    <label @click="remove(index)">X</label>
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

    .file-list li label {
        color: red;
        font-weight: 900;
    }

    input[type='file'] {
        display: none;
    }
</style>

<script>
    import { defineComponent, ref } from 'vue';
    import UploadFile from './UploadFile.vue';

    export default defineComponent({
        props: {
            id: {
                type: String,
                default: 'upload-files',
                required: true,
            },
            accept: String,
            label: {
                type: String,
                default: 'Select',
            },
            title: {
                type: String,
                default: 'Files to upload',
            },
            class: {
                type: String,
                default: '',
            },
        },
        emits: ["input", "update:modelValue"],
        setup(props, { emit }) {
            const fileList = ref([]);
            const filesList = ref([]);

            function recreateList() {
                const fs = [];
                let i = 0;
                for (const f of fileList.value) {
                    f.index = i++;
                    fs.push(f.file);
                }
                filesList.value = fs;
                emit('input', fs);
                emit('update:modelValue', fs)
            }

            function add(file) {
                fileList.value.push(file);
                recreateList();
            }

            function remove(fileIndex) {
                fileList.value = fileList.value.filter((el) => el.index !== fileIndex);
                recreateList();
            }

            function onChange(e) {
                for (const el of e.target.files) {
                    let ext = '.' + el.name.split('.').pop();
                    if (props.accept.indexOf(ext) >= 0) {
                        const file = new UploadFile(el, fileList.value.length);
                        add(file);
                    }
                }
                recreateList();
            }

            function selectFiles() {
                let e = document.getElementById(props.id).children[1];
                e.click();
            }

            return {
                fileList,
                files: filesList.value,
                remove,
                onChange,
                selectFiles,
            };
        },
    });
</script>
