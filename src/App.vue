<template>
  <div id="app">
    <Gauge :value="hpval" :max="100" :dangerth="20" />
    <input type="number" v-model="hpdiffval" min="-100" max="100" />
    <input type="text" v-model="tmsg" />
    <button @click="submit">確定</button><br />
    <button @click="reset">Reset</button>
    <div class="log">
      {{ log }}
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Gauge from "./components/Gauge.vue";

@Component({
  components: {
    Gauge
  }
})
export default class App extends Vue {
  public hpval = 100;
  public log = "";
  public hpdiffval = 0;
  public tmsg = "";
  public submit() {
    this.addLog(this.hpdiffval * 1, this.tmsg);
  }
  public reset() {
    this.hpval = 100;
    this.log = "";
  }
  public addLog(HPDiff: number, msg: string) {
    this.log += msg + "\n";
    this.hpval += HPDiff;
    if (this.hpval < 0) this.hpval = 0;
    if (this.hpval > 100) this.hpval = 100;
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
.log {
  white-space: pre-line;
}
</style>
