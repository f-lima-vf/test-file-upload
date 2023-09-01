<template>
    <div v-bind:id="id">
        <input class="file-input" type="file" multiple v-bind:disabled="disabled" 
            v-bind:accept="accept" @input="onChange($event)">
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
    import { defineComponent, ref, onMounted } from 'vue';
    import UploadFile from './UploadFile.vue';

    export default defineComponent({
        props: {
            id: {
                type: String,
                required: true,
            },
            accept: String,
        },
        emits: ["input", "update:modelValue"],
        setup(props, { emit }) {
            const fileList = ref([]);

            function add(file) {
                fileList.value.push(file);
            }

            function remove(fileIndex) {
                fileList.value = fileList.value.filter((el) => el.index !== fileIndex);
            }

            function onChange(e) {
                for (const el of e.target.files) {
                    const file = new UploadFile(el);
                    add(file);
                }
                const fs = [];
                for (const f of fileList.value) {
                    fs.push(f.file);
                }
                this.files = fs;
                emit('input', fs);
                emit('update:modelValue', fs)
                // this.modelValue = fs; // You might need to emit an event if you're using v-model
                // this.processFiles(e.target.files);
                //e.preventDefault();
            }

            onMounted(() => {
                // window.addEventListener('remove', this.onRemove);
            });

            return {
                fileList,
                files: [],
                remove,
                onChange,
            };
        },
    });
</script>
