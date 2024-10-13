<script>
export default {
  name: "answer",
  props: {
    text: {
      type: String,
      required: true,
    },
  },
  data() {
    return {};
  },
  mounted(props) {
    console.log("Defining answer!");
  },
  setup() {
    return {};
  },
};
</script>

<template>
  <div class="box">
    <div>{{ text }}</div>
  </div>
</template>

<style>
.box {
  background-color: red;
  margin: 20px;
  padding: 20px;
}
</style>
