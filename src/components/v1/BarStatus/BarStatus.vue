<template>
  <div
    class="RfContainer"
    :style="{ width: `${life <= 0 ? 0 : life}%`, backgroundColor: colorStatus }"
  ></div>
  <div class="RfLoad">
    <span>{{ life <= 0 ? 0 : life}}%</span>
  </div>
</template>

<script>
export default {
  name: "RfBarStatus",
  props: {
    life: { type: Number, default: 100 },
    colorStatus: { type: String, default: "#00ff00" },
  },
};
</script>

<style lang="scss">
.RfContainer {
  width: auto;
  height: 40px;
}
.RfLoad {
  padding-top: 10px;
  font-size: 2em;
}
</style>