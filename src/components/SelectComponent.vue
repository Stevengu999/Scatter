<template>
    <section class="select" :class="{'open':open}">
        <figure class="open-option" v-on:click="toggle">{{selectedOption}}</figure>
        <figure class="arrow" v-on:click="toggle"><i class="fa fa-caret-down"></i></figure>

        <section class="options" :class="{'show':open}">
            <figure class="option" v-on:click="selectOption(option)" v-for="option in options">{{option}}</figure>
        </section>
    </section>
</template>
<script>
    export default {
        data() { return {
            open:false,
            selectedOption:(this.forceSelectedOption) ? this.forceSelectedOption : this.options[0]
        };
        },
        methods: {
            close:function(){this.open = false;},
            toggle:function(){this.open = !this.open;},
            selectOption:function(option){ this.selectedOption = option; this.close(); },
            changed:function(){ this.$emit('changed', this.selectedOption) }
        },
        props: ['options', 'forceSelectedOption'],
        watch: {
            selectedOption: function(n,o) { this.changed(); },
            forceSelectedOption: function(n,o) { this.selectedOption = this.forceSelectedOption; },
        }
    };
</script>