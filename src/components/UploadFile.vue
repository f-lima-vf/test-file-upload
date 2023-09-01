<script>
import { ref, computed } from 'vue';

export default function UploadFile(file) {
  const _file = ref(file);
  const _index = ref(-1);
  const _name = ref(file.name);
  const _type = ref(file.type);
  const _url = ref(URL.createObjectURL(file));
  const _size = ref(file.size);
  const _bytesRead = ref(0);
  const _bytes = ref([]);

  const fileRef = computed(() => _file.value);
  const index = computed({
    get: () => _index.value,
    set: (value) => {
      _index.value = value;
    },
  });
  const name = computed({
    get: () => _name.value,
    set: (value) => {
      _name.value = value;
    },
  });
  const type = computed({
    get: () => _type.value,
    set: (value) => {
      _type.value = value;
    },
  });
  const url = computed({
    get: () => _url.value,
    set: (value) => {
      _url.value = value;
    },
  });
  const size = computed({
    get: () => _size.value,
    set: (value) => {
      _size.value = value;
    },
  });
  const bytesRead = computed({
    get: () => _bytesRead.value,
    set: (value) => {
      _bytesRead.value = value;
    },
  });
  const bytes = computed({
    get: () => _bytes.value,
    set: (value) => {
      _bytes.value = value;
    },
  });

  const percentDone = computed(() => Math.ceil(_bytesRead.value * 100 / _size.value));

  return {
    file: fileRef,
    index,
    name,
    type,
    url,
    size,
    bytesRead,
    bytes,
    percentDone,
  };
}
</script>
