<script>
import { ref, computed } from 'vue';

export default function UploadFile(f, idx) {
  const _file = ref(f);
  const _index = ref(idx);
  const _name = ref(f.name);
  const _type = ref(f.type);
  const _url = ref(URL.createObjectURL(f));
  const _size = ref(f.size);

  const file = computed(() => _file.value);
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

  return {
    file,
    index,
    name,
    type,
    url,
    size,
  };
}
</script>
