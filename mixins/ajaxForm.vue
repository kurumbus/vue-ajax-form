<script>
    export default {
        methods: {
            submitForm: function(el) {
                el.preventDefault();    // Prevent regular form submission
                let method = this._vnode.elm.method;
                let action = this._vnode.elm.action;
                let inputs = this.$el.getElementsByTagName('input');  // Get all inputs
                inputs = Array.prototype.slice.call(inputs);
                inputs = inputs.filter(input => {return input.type != 'submit'});  // Except submit
                let textareas = this.$el.getElementsByTagName('textarea'); // get textareas
                let combined = [].concat(Array.prototype.slice.call(inputs), Array.prototype.slice.call(textareas));
                combined = Array.prototype.slice.call(combined);

                let data = combined.map((input) => {
                    let ar = [];
                    ar[input.name] = input.value;
                    return ar;
                });
                let newArray = data.reduce(function (r, a) {
                    return Object.assign(r, a);
                }, {});   // map array to turn it into an object {name: value, name2: value2}



                Vue.axios[method](action, newArray).then((response) => {
                    return this.handleResponse(response); // pass response to to handleResponse method of the component
                });
            },
        }
    };
</script>
