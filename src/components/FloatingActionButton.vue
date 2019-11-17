<template>
    <base-button class="floating-action-button" v-bind="$attr" v-on="$listeners">
        <slot></slot>
    </base-button>
</template>

<script>
import BaseButton from './BaseButton'

export default {
    components: {
        BaseButton
    }
}
</script>

<style>
    .floating-action-button {
        width: 64px;
        height: 64px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 10000px;
        padding: 0;
    }
</style>