<template>
  <button class="base-button" v-bind="$attrs" v-on="$listeners" @click="addRipple($event)">
        <slot></slot>

        <transition-group 
            name="list" 
            class="ripple-container" 
            tag="div">  
            <div v-for="ripple in ripples" :key="ripple.id" class="ripple" :style="`transform: translate(${ripple.x}px, ${ripple.y}px)`"></div>
        </transition-group>
  </button>
</template>

<script>
export default {
    props: {
        duration: {
            type: Number,
            default: 2000
        }
    },
    data () {
        return {
            ripples: []
        }
    },
    methods: {
        clamp (x, a, b) {
            return x < a ? a : x >= b ? b : x
        },
        addRipple (e) {
            
            const { clientX, clientY } = e
            const { x, y, width, height } = this.$el.getBoundingClientRect ()

            const xPos = this.clamp(clientX - x, 0, width) 
            const yPos = this.clamp(clientY - y, 0, height)

            const ripple = {
                id: (Math.random () * 100).toString (),
                x: xPos - (width / 2),
                y: yPos - (height / 2)
            }

            ripple.timeOut = setTimeout (() => {
                this.ripples = this.ripples.filter (r => 
                    r.id !== ripple.id
                )
            }, this.duration)

            this.ripples = [...this.ripples, ripple]
        }
    }
}
</script>

<style>
    .list-enter-active/*, .list-leave-active*/ {
        transition: clip-path .5s, opacity .5s;
    }
    .list-enter {
        clip-path: circle(0%);
        opacity: 1 !important;
    }

    .list-enter-to {
        clip-path: circle(100%);
        opacity: 0 !important;
    }

    .base-button {
        border: none;
        color: white;
        background: rgba(0, 150, 136);
        font-family: 'Roboto', sans-serif;
        font-size: 16px;
        padding: .5em 1.2em;
        border-radius: 4px;

        /** This rule is mandatory */
        position: relative;

        outline: none;

        /** This rule is mandatory */
        overflow: hidden;
    }

    /** Those rules are mandatory */
    .ripple-container {
        position: absolute;

        top: 0;
        right: 0;
        left: 0;
        bottom: 0;

        /** This rule is mandatory */
        overflow: hidden;

        /** This rule is mandatory even if the border-radius is greater than 1px */
        border-radius: 1px;
    }

    .ripple {
        /** This rule is mandatory */
        position: absolute;

        /** Those rules are mandatory */
        top: -100%;
        right: -100%;
        bottom: -100%;
        left: -100%;

        background: rgba(0,0,0,0.5);
        
        /** This rule is mandatory */
        opacity: 0;
    }
</style>