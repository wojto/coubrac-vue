<template>
    <span class="input-editable">
        <span class="current" @click="handleClick" :style="{ display: in_edit_mode ? 'none' : 'inline' }">
            {{ value }}
        </span>
        <input title="" ref="textInput" :value="value" @blur="handleBlur" @keyup="handleKeyUp"
               :style="{ display: in_edit_mode ? 'inline' : 'none' }" />
    </span>
</template>

<script>
    export default {
        name: 'InputEditable',
        props: {
            value: {
                type: String,
                required: false
            }
        },
        data()
        {
            return {
                in_edit_mode: false
            }
        },
        methods: {
            handleKeyUp(event) {
                if ('Enter' === event.key) {
                    this.handleBlur(event);
                }
            },
            handleClick() {
                this.in_edit_mode = true;
                setTimeout(() => this.focus(), 0);
            },
            handleBlur(event) {
                this.$emit('handleChange', event.target.value);
                this.in_edit_mode = false;
            },
            focus() {
                this.$refs.textInput.focus();

                let len = this.$refs.textInput.value.length;
                this.$refs.textInput.setSelectionRange(len, len);
            }
        }
    }
</script>

<style scoped>
.input-editable {
    color: #ff3333;
    text-decoration: underline;
    cursor: pointer;
}
input {
    border: none;
    outline: none;
    height: 1em;
    font-weight: bold;
}
</style>
