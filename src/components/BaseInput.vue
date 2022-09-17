<template>
    <label>{{label}}</label>
    <input :value="modelValue" class="form-control" @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="label" v-bind="$attrs">
</template>

<script>
export default {
    name: 'BaseInput',
    props: {
        label: {
            type: String,
            default: '',
        },
        modelValue: {
            type: [String, Number],
            default: ''
        },
        mask: {
            type: String,
            required: false
        }
    }
}
</script>

<style lang="scss" scoped>

</style>