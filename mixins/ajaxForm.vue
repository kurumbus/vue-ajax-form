<script>
    export default {
        methods: {
            submitForm: function(el) {
                el.preventDefault();
                let method = this._vnode.elm.method;
                let action = this._vnode.elm.action;
                let inputs = this.$el.getElementsByTagName('input');
                inputs = Array.prototype.slice.call(inputs);
                inputs = inputs.filter(input => {return input.type != 'submit'});
                let textareas = this.$el.getElementsByTagName('textarea');
                let combined = [].concat(Array.prototype.slice.call(inputs), Array.prototype.slice.call(textareas));
                combined = Array.prototype.slice.call(combined);

                let data = combined.map((input) => {
                    let ar = [];
                    ar[input.name] = input.value;
                    return ar;
                });
                let newArray = data.reduce(function (r, a) {
                    return Object.assign(r, a);
                }, {});
                console.log(newArray);



                Vue.axios[method](action, newArray).then((response) => {
                    data.res = response;
                });
            },
        }
    };
</script>
