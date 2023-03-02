<script>

    export default{
        props: {
            placeholder: {
                type: String,
                default: ""
            },
            required: {
                type: Boolean,
                default: false
            },
            type: {
                type: String,
                default: "text"
            },
            id: {
                type: String,
                default: null
            }
        }
    }

</script>

<template>
    <input
        :id="id"
        :type="type"
        :placeholder="placeholder"
        :required="required"
        v-model="modelValue"
        class="border-0 bg-stone-100 rounded-md p-2"
    >
</template>