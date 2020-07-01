<template>
  <div>
    <div  v-for="control in modal.controls" :key="control.id">
      <CustomLabel v-if="control.type=='label'" :control="control" />
      <CustomInput :control="control" />
    </div>
  </div>
</template>


<script>
import CustomLabel from "./CustomLabel";
import CustomInput from "./CustomInput";

export default {
  components: {
    CustomLabel,
    CustomInput,
   
  },
  props: {
    modal: Object
  }
};
</script>


