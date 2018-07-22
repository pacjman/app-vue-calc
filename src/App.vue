
<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <div class="greeting"><span>Greetings</span></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
@Component({
  components: { }
})
export default class App extends Vue {
  title: string;
  constructor() {
    super();
    this.title = 'My Frist Vue App';
  }
}
</script>

<style>

  .greeting {
    font-size: 40px;
  }

</style>
