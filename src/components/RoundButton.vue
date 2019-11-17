<template>
    <base-button class="round-button" v-bind="$attrs" v-on="$listeners">
        <slot></slot>
    </base-button>
</template>

<script>
import BaseButton from './BaseButton'

export default {
    components: { BaseButton }
}
</script>

<style>
    .round-button {
        border-radius: 10000px;
    }

    .round-button .ripple-container {
        overflow: hidden;
    }
</style>