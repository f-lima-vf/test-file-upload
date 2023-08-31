<script>
    export default class {
        constructor(file) {
            this._file = file;
            this._index = -1;
            this._name = file.name;
            this._type = file.type;
            this._url  = URL.createObjectURL(file);
            this._size = file.size;
            this._bytesRead = 0;
            this._bytes = [];
        }
        get file() {
            return this._file;
        }
        set index(value) {
            this._index = value;
        }
        get index() {
            return this._index;
        }
        set name(value) {
            this._name = value;
        }
        get name() {
            return this._name;
        }
        set type(value) {
            this._type = value;
        }
        get type() {
            return this._type;
        }
        set url(value) {
            this._url = value;
        }
        get url() {
            return this._url;
        }
        set size(value) {
            this._size = value;
        }
        get size() {
            return this._size;
        }
        set bytesRead(value) {
            this._bytesRead = value;
        }
        get bytesRead() {
            return this._bytesRead;
        }
        set bytes(value) {
            this._bytes = value;
        }
        get bytes() {
            return this._bytes;
        }
        get percentDone() {
            return Math.ceil(this._bytesRead * 100 / this._size);
        }
    }
</script>
