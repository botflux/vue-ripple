<template>
  <div id="app">
    <base-button>
      Click me
    </base-button>

    <round-button>
      Click me
    </round-button>

    <floating-action-button>
      <i class="material-icons">add</i>
    </floating-action-button>
  </div>
</template>

<script>
import BaseButton from './components/BaseButton'
import RoundButton from './components/RoundButton'
import FloatingActionButton from './components/FloatingActionButton'

export default {
  name: 'app',
  components: {
    BaseButton, RoundButton, FloatingActionButton
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
