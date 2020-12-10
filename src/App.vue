<template>
  <div id="app">
    <validate-component :id="1">
      <HelloWorld slot="some" msg="some">
        <validate-component slot="valComp" :id="2"></validate-component>
        <validate-component slot="valComp" :id="2.1"></validate-component>
      </HelloWorld>
      <HelloWorld slot="some" msg="some">
        <validate-component slot="valComp" :id="3">
          <validate-component slot="valComp" :id="4" />
        </validate-component>
      </HelloWorld>
      <validate-component slot="valComp" :id="5"></validate-component>
    </validate-component>
    <validate-component :id="6"></validate-component>
  </div>
</template>

<script>
import validateComponent from './components/validateComponent.vue'
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    "validate-component": validateComponent,
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
