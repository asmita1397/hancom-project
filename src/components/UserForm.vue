<template>
  <div>
    <div
      ref="nnn"
      v-bind:key="index"
      v-for="(modal,index) in this.modals"
      :style="modal.style"
      @click="make(modal)"
      @mousedown="dragMouseDown($event,modal.id)"
    >
      <p :style="modal.headerText">
        {{modal.name}}{{modal.id}}
        <button
          :style="modal.closeButton"
          v-on:click="closeWindow(modal)"
        >x</button>
      </p>
      <div :style="modal.inner" ref="pos" @click="createTool($event,modal.id,'mmmm')">
        <p :style="modal.innerHeaderText">
          {{modal.name}}{{modal.id}}
          <button :style="modal.closeInnerButton" disabled>x</button>
        </p>
        <div v-for="control in modal.controls" :key="control.id">
          <Label :control="control" />
        </div>
      </div>
    </div>
    <Label />
    <Dragable ref="child" />
  </div>
</template>

<script>
import Dragable from "./Dragable";
import Label from "./Label";

export default {
  name: "UserForm",
  components: {
    Dragable,
    Label
  },
  data() {
    return { refer: "" };
  },
  props: {
    modals: Array,
    selected: String
  },

  methods: {
    make(modal) {
      console.log("hiiii", modal);
      this.$emit("makeActive", modal);
    },
    closeWindow(modal) {
      this.$emit("closeWindow", modal);
    },
    dragMouseDown(event, data) {
      event.preventDefault();
      this.refer = data;
      console.log("hhhhhh", this.refer);
      this.$refs.child.dragMouseDown(event);
      document.onmousemove = this.elementDrag;
      document.onmouseup = this.closeDragElement;
    },
    elementDrag: function(event) {
      event.preventDefault();
      this.$refs.child.elementDrag(event, this.$refs.nnn[this.refer - 1]);
    },
    closeDragElement: function(event) {
      this.$refs.child.closeDragElement(event);
    },
    createTool(e, pos, con) {
      console.log("contol", e);
      /*  this.control.style.top = `${e.offsetY}px`;
      this.$refs.container1.appendChild(instance.$el).style.left = `${e.offsetX}px`; */
      console.log("nnnn", pos);
      console.log(this.selected);

      if (this.selected == "label") {
        const tool = {
          id: this.modals[pos - 1].controls.length + 1,
          name: "Label",
          type: "label",
          attributes: {
            value: "Good Morning"
          },
          style: {
            position: "absolute",
            left: `${e.layerX}px`,
            top: `${e.layerY}px`,
            width: "100px",
            height: "40px",
            resize: "both",
            overflow: "auto",
            zIndex: "1",
            border: "1px solid black"
          }
        };
        if (e.layerY > 54) {
          this.$emit("addControl", tool, pos, con);
        }
      }
    }
  }
};
</script>




