<template>
  <div>
    
    <input v-if="control" :style="control.style">{{control.name}} />
  </div>
</template>

<script>
export default {
  name: "customInput",
  props: {
    control: Object
  }
};
</script>