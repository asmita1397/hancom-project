<template>
  <label :style="control.style">{{control.name}}</label>
</template>

<script>
export default {
  props: ["control"]
};
</script>

<style scoped>
</style>