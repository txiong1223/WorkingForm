<template>
    <div class="form-group">
        <label>{{label}}</label>
        <select class="form-control" @change="$emit('input', $event.target.value)">
            <option v-for="opt in options" :key="opt.modelValue" :value="opt.modelValue"
                :selected="modelValue===opt.modelValue">{{opt.label
                || 'No label'}}</option>
        </select>
    </div>
</template>

<script>
export default {
    name: 'BaseSelect',
    props: {
        label: {
            trype: String,
            default: ''
        },
        options: {
            type: Array,
            validator(opts) {
                return !opts.find(opt => typeof opt !== 'object')
            }
        },
        modelValue: {
            type: [String, Number],
            default: ''
        }
    },
}
</script>

<style lang="scss" scoped>

</style>