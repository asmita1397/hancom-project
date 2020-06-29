<template>
  <div class="container" ref="draggableContainer" id="draggable-container">
    <div :style="style" @mousedown="dragMouseDown" @click="toolBoxClick">
      <span class="dot">ToolBox</span>
    </div>
    <hr />
    <div>
      <span class="content" @click="handleClick('label')">
        <Icon />
      </span>
      <span class="content" @click="handleClick('arrow')">
        <Icon />
      </span>
    </div>
    <Dragable ref="child" />
  </div>
</template>
 
<script>
import Icon from "./Icons";
import Dragable from "./Dragable";
export default {
  name: "ToolBox",
  components: {
    Icon,
    Dragable
  },
  data() {
    return {
      style: {
       
        cursor: "pointer",
        zIndex: "0",
        padding: "10px",
        background: "dimgrey",
        borderTopLeftRadius: " 4px",
        borderTopRightRadius: "4px",
        height: "20%",
        left: "0"
      }
    };
  },
  props: {
    prevModalZIndex:Number
  },
  methods: {
    dragMouseDown(event) {
      event.preventDefault();
      console.log("tool", this.prevModalZIndex,this.style.zIndex);
     /*  this.style.zIndex=this.prevModalZIndex++ */
      this.$refs.child.dragMouseDown(event);
      document.onmousemove = this.elementDrag;
      document.onmouseup = this.closeDragElement;
    },

    elementDrag: function(event) {
      this.$refs.child.elementDrag(event, this.$refs.draggableContainer);
    },
    closeDragElement: function(event) {
      this.$refs.child.closeDragElement(event);
    },
    handleClick(tool) {
      console.log("tool", tool);
      
      this.$emit("selectedTool", tool);
    },
    toolBoxClick()
    {
      this.style.zIndex=this.prevModalZIndex+10
    }
  }
};
</script>



<style scoped>
#draggable-container {
  position: absolute;
  z-index: 100;
  /*  background-color: #f1f1f1; */
  text-align: center;
  border: 1px solid #d3d3d3;
  width: 30%;
  background-color: dimgrey;
}

#draggable-header {
  padding: 10px;
  cursor: pointer;
  z-index: 100;
}

.dot {
  display: inline-block;
  float: left;
  color: white;
}

.container {
  border: 3px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}

.top {
  padding: 10px;
  background: dimgrey;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  height: 20%;
  left: 0;
}

.content {
  display: inline-block;
  float: left;
}
</style>