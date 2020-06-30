<template>
  <div>
    <label  v-if="control" :style="control.style">{{control.name}}</label>
  </div>
</template>

<script>
export default {
  name: "Label",
  props: {
    control: Object
  }
};
</script>


