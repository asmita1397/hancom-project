<template>
  <label class="label-style">
    <slot>{{text}}</slot>
  </label>
</template>

<script>
export default {
  name: 'label',
  props:{
      text:String
  },
  
}
</script>

<style scoped>
.label-style
{
  border: 1px solid;
  padding: 10px;
  position:relative;
  top:10px

}
</style>
