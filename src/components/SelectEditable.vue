<template>
    <span class="select">
        <span class="selected" @click="handleSelectedClick" @mouseleave="handleMouseLeave">
            {{ selected_name }}
        </span>
        <span class="options" :style="{ display: open ? 'block' : 'none' }" @mouseleave="handleMouseLeave"
             @mouseenter="handleMouseEnter">
            <span v-for="option in options" :key="option.value" :class="[selected_value === option.value ? 'selected'
                : '']" @click="handleClick" :data-value="option.value">
                {{ option.name }}
            </span>
        </span>
    </span>
</template>

<script>
    export default {
        name: 'SelectEditable',
        props: {
            options: {
                type: Array,
                required: true
            },
            selected: {
                type: String,
                required: true
            },
            handleChange: {
                type: String,
                required: false
            }
        },
        data()
        {
            return {
                timer: 0,
                open: false
            }
        },
        computed: {
            selected_name: function () {
                return this.getNameOfValue(this.options, this.selected)

            },
            selected_value: function () {
                return this.selected
            }
        },
        methods: {
            getNameOfValue(options, selected) {
                let result;
                options.map(function(option){
                    if (option.value === selected) {
                        result = option.name;
                    }
                });
                return result;
            },
            handleClick(event) {
                this.$emit('handleChange', event.target.getAttribute('data-value'));
                this.open = false;
            },
            handleSelectedClick(event) {
                this.open = true;
            },
            handleMouseEnter() {
                if (this.timer) {
                    clearTimeout(this.timer);
                }

                this.open = true;
            },
            handleMouseLeave() {
                this.timer = setTimeout(function(self) {
                    self.open = false;
                }, 100, this);
            }
        }
    }
</script>

<style scoped>
.select {
    display: inline-block;
    text-decoration: underline;
    position: relative;
    color: #ff3333;
    cursor: pointer;
}
.options {
    position: absolute;
    left: -30px;
    top: 20px;
    z-index: 1;
    cursor: pointer;
    background-color: #fff;
    border: 1px solid #ff3333;
    border-radius: 5px;
    line-height: 2em;
    color: #ff3333;
}
.options span {
    display: table-cell;
    padding: 2px 4px 0;
}
.options span:not(:first-child) {
    border-left: 1px solid #ff3333;
}
.options span.selected {
    background-color: #ff3333;
    color: #fff;
}
</style>
