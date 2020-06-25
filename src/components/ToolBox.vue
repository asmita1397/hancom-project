<template>
    
  <div class="container" ref="draggableContainer" id="draggable-container">
      <div class="top" id="draggable-header" @mousedown="dragMouseDown">
        
        <span class="dot">ToolBox</span>
      </div>
     <hr>
      <div  >
          <span class="content"  @click="handleClick('label')"><Icon /></span>
          <span class="content" @click="handleClick('arrow')"><Icon /></span>
          
      </div>
    </div>
</template>


<script>
import  Icon from "./Icons"
export default {
  name: 'DraggableDiv',
  components:{
     Icon
  },
  data: function () {
    return {
      positions: {
        clientX: undefined,
        clientY: undefined,
        movementX: 0,
        movementY: 0
      }
    }
  },
  methods: {
    dragMouseDown: function (event) {
      event.preventDefault()
      // get the mouse cursor position at startup:
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      document.onmousemove = this.elementDrag
      document.onmouseup = this.closeDragElement
    },
    elementDrag: function (event) {
      event.preventDefault()
      this.positions.movementX = this.positions.clientX - event.clientX
      this.positions.movementY = this.positions.clientY - event.clientY
      this.positions.clientX = event.clientX
      this.positions.clientY = event.clientY
      // set the element's new position:
      this.$refs.draggableContainer.style.top = (this.$refs.draggableContainer.offsetTop - this.positions.movementY) + 'px'
      this.$refs.draggableContainer.style.left = (this.$refs.draggableContainer.offsetLeft - this.positions.movementX) + 'px'
    },
    closeDragElement () {
      document.onmouseup = null
      document.onmousemove = null
    },
   handleClick(data)
   {
       console.log(data)
       this.$emit('handleLabel',data) 
   }

  }
}
</script>



<style scoped>
#draggable-container {
  position: absolute;
  z-index: 9;
 /*  background-color: #f1f1f1; */
  text-align: center;
  border: 1px solid #d3d3d3;
  width:30%;
  background-color: dimgrey;
}

#draggable-header {
  padding: 10px;
  cursor: move;
  z-index: 10;
  
}


.dot {
  display: inline-block;
  float:left;
  color:white;
}

.container {
  border: 3px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;

}

.top {
  padding: 10px;
  background:dimgrey;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  height:20%;
  left:0;
}

.content {
  display: inline-block;
  float :left
}

</style>