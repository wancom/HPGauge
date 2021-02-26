<template>
  <div id="app">
    <div v-for="(v, i) in hpval" :key="i">
      <Gauge :value="hpval[i]" :max="hpmax[i]" :dangerth="hpdangerth[i]" />
      <input type="number" v-model="hpdiffval[i]" min="-100" max="100" />
      <input type="text" v-model="tmsg[i]" />
      <button @click="submit(i)">確定</button><br />
      <button @click="reset(i)">Reset</button>
      <div class="log">
        {{ log[i] }}
      </div>
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
  public hpval = [100, 100];
  public hpmax = [100, 100];
  public hpdangerth = [20, 20];

  public log = ["", ""];

  public hpdiffval = [0, 0];
  public tmsg = ["", ""];

  public submit(i: number) {
    this.addLog(i, this.hpdiffval[i] * 1, this.tmsg[i]);
  }
  public reset(i: number) {
    this.hpval.splice(i, 1, 100);
    this.log.splice(i, 1, "");
  }
  public addLog(i: number, HPDiff: number, msg: string) {
    this.log.splice(i, 1, this.log[i] + msg + "\n");
    this.hpval.splice(i, 1, this.hpval[i] + HPDiff);
    if (this.hpval[i] < 0) this.hpval.splice(i, 1, 0);
    if (this.hpval[i] > 100) this.hpval.splice(i, 1, 100);
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
