<template>
  <div>
    <div :style="parent">
      <template>
      <vue-draggable-resizable
        v-for="control in modal.controls"
        :key="control.id"
        :w="parseInt(control.style.width)"
        :h="parseInt(control.style.height)"
        :x="parseInt(control.style.left)"
        :y="parseInt(control.style.top)"
        :parent="true"
        @resizing="(x,y,width,height)=>onResize(control,x,y,width,height)"
        @dragging="onDrag"
        @deactivated="onDeactivated"
        @activated="onActivated"
        ref="vdr"
      >
        <input  :style="control.style" ref="i" @click="inputClick" />
        <!--  <label :style="v">kkkkkk</label> -->
        <!--  <button :style="v">jjjjjjj</button> -->
      </vue-draggable-resizable>
       </template>
    </div>
   
  </div>
</template>


<script>
/* import CustomLabel from "./CustomLabel";
import CustomInput from "./CustomInput"; */
import VueDraggableResizable from "./vue-draggable-resizable";

export default {
  components: {
    /*  CustomLabel,
    CustomInput, */
    VueDraggableResizable
  },
  data() {
    return {
      v: {
        width: "50px",
        height: "20px",
        left: 0,
        right: 0,
        border: "1px dotted black"
      },

      parent: {
        width: "98%",
        height: "98%",
        position: "absolute",
        backgroundColor: ""
      }
    };
  },
  props: {
    modal: Object
  },
  ready() {
    console.log("kkkkkppppp");
  },
  methods: {
    onResize(control, x, y, width, height) {
      console.log("nnnn");
      control.style.width = `${width}px`;
      control.style.height = `${height}px`;
      control.style.left = `${x}px`;
      control.style.right = `${y}px`;
      console.log("jjjjjjjjjjj", x, y, width, height, control);
      
      
      console.log();
    },
    onDrag: function(x, y) {
      this.v.left = `${x}px`;
      this.v.top = `${y}px`;
    },
    onDeactivated() {
      console.log("deactive");
    },
    onActivated() {
      console.log(this.$refs.vdr);
      console.log("active");
    },

    inputClick() {
      this.$refs.i.focus();
    }
  }
};
</script>


<style  scoped>
</style>