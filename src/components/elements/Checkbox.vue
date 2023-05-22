<template>
    <div :class="['e-checkbox',{'e-checkbox--checked': state}]" v-on:click="$emit('check', !state)">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
            <path
                d="M470.6 105.4c12.5 12.5 12.5 32.8 0 45.3l-256 256c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0L192 338.7 425.4 105.4c12.5-12.5 32.8-12.5 45.3 0z"/>
        </svg>
    </div>
</template>
<script>
    export default {
        props: {
            state: {
                default: () => false,
                type: Boolean
            }
        }
    }
</script>
<style lang="scss">
    .e-checkbox {
        width: 18px;
        height: 18px;
        border-radius: 18px;
        border: 1px solid $borderColor;
        display: inline-block;
        svg {
            fill: $borderColor;
            opacity: 0;
            transition: opacity .5s;
            max-width: 100%;
        }
        &--checked{
            svg {
                opacity: 1;
            }
        }
    }
</style>