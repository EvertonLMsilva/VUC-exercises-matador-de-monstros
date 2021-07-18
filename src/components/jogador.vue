<template>
  <div class="JogadorContainer" :style="{ width: width }">
    <span class="title">{{ namePlayer }}</span>
    <RfBarStatus :colorStatus="lowLife(life)" :life="life" />
  </div>
</template>
<script>
import RfBarStatus from "./v1/BarStatus/BarStatus.vue";

export default {
  name: "jogador",
  props: {
    namePlayer: { type: String, default: "Player" },
    life: { type: Number, default: 100 },
    width: { type: String, default: "250px" },
  },
  components: {
    RfBarStatus,
  },
  methods: {
    lowLife(value) {
      if (value <= 20) return "#ff0000";
    },
  },
};
</script>

<style lang="scss">
.JogadorContainer {
  display: flex;
  justify-content: center;
  flex-direction: column;

  .title {
    margin-bottom: 20px;
    font-size: 2em;
  }
}
</style>