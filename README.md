# vue-ajax-form
A mixin for vue to submit any form asynchronously

## Usage
Add as a mixin to a form component:

```javascript
<script>
    import AjaxForm from '../mixins/ajaxForm.vue';

    export default {
        data: function() {
            return {}
        },
        mixins: [AjaxForm],
    };
</script>
```

You should also add on-submit event:
```javascript
 <form method="POST" v-on:submit="submitForm" action="...">
```

Mixin will prevent default form submission and submit it asynchronously with axios
