<template>
  <div class="gauge">
    <h1>HP: {{ value }}</h1>
    <div class="gauge-container">
      <div class="gauge-container-barborder"></div>
      <div
        class="gauge-container-bar"
        :class="value > dangerth ? '' : 'danger'"
      ></div>
      <div
        class="gauge-container-barover"
        :style="{
          width: 300 - gaugeSize() + 'px',
          'margin-left': 5 + gaugeSize() + 'px'
        }"
      ></div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

const MAXSIZE = 300;

@Component
export default class HelloWorld extends Vue {
  @Prop() private value!: number;
  @Prop() private max!: number;
  @Prop() private dangerth!: number;
  private gaugeSize(): number {
    return MAXSIZE * (this.value / this.max);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gauge-container {
  height: 14px;
  margin: 10px;
  border-radius: 24px;
}
.gauge-container-barborder {
  position: absolute;
  width: 304px;
  height: 14px;
  border: black 3px solid;
  border-radius: 24px;
  z-index: 1002;
}
.gauge-container-barover {
  position: absolute;
  height: 10px;
  margin: 5px;
  background: white;
  z-index: 1001;
  transition: 0.3s;
}
.gauge-container-bar {
  position: absolute;
  width: 300px;
  height: 10px;
  margin: 5px;
  background: green;
  border-radius: 20px;
  z-index: 1000;
}
.danger {
  background: red;
}
</style>
