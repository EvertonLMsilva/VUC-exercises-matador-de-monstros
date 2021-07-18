<template>
  <input
    class="RfButtonContainer"
    type="button"
    :value="nameButton"
    :style="setColor(color)"
  />
</template>

<script>
export default {
  name: "RfButton",
  props: {
    nameButton: { type: String, default: "Button" },
    color: { type: String, default: "primary" },
  },
  methods: {
    setColor(value) {
      let selectColor = "";

      switch (value) {
        case "primary":
          selectColor = "#0000ff";
          break;
        case "secondary":
          selectColor = "#00ff00";
          break;
        case "warning":
          selectColor = "#ff0000";
          break;
        case "alert":
          selectColor = "#ff7700";
          break;
        case "neutral":
          selectColor = "#cccccc";
          break;

        default:
          selectColor = "#010ce6";
          break;
      }
      
      return {
        backgroundColor: selectColor,
      };
    },
  },
};
</script>

<style lang="scss" scope>
.RfButtonContainer {
  background-color: #0032d4;
  color: #ffffff;
  width: auto;
  padding: 15px 25px 15px 25px;
  font-size: 1.5em;
  border: 1px #ccc solid;
  border-radius: 15px;
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.5);
  cursor: pointer;
}
</style>