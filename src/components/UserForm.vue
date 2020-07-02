<template>
  <div>
    <div v-bind:key="index" v-for="(modal,index) in userForms">
      <div
        :style="modal.outerWindowStyle.container"
        ref="outerWindowContainerRef"
        @click="make(modal)"
      >
        <div :style="modal.outerWindowStyle.top" @mousedown="dragMouseDown($event,modal.id)">
          <span>Book1 {{modal.name}}{{modal.id}} (UserForm)</span>
         
          <button :style="modal.outerWindowStyle.closeButton" v-on:click="closeWindow(modal)">x</button>
        </div>

        <div :style="modal.innerWindowStyle.container" v-resize @resize="onResize($event,modal.id)">
          <div :style="modal.innerWindowStyle.top">
            <span>{{modal.name}}{{modal.id}}</span>
            <button :style="modal.innerWindowStyle.closeButton" disabled>x</button>
          </div>
          <div
            ref="pos"
            :style="modal.innerWindowStyle.innerContainer"
            @click="createTool($event,modal.id)"
          >
            <UserFormControl :modal="modal" />
          </div>
        </div>
      </div>
    </div>
    <Dragable ref="child" />
  </div>
</template>

<script>
import Dragable from "./Dragable";

import customLabelData from "./CustomLabel";
import UserFormControl from "./UserFormControl";

export default {
  name: "UserForm",
  components: {
    Dragable,
    UserFormControl
  },
  data() {
    return { refer: "" };
  },
  props: {
    userForms: Array,
    selectedControl: String
  },

  methods: {
    onResize(e, userFormId) {
      this.$emit("innerWindowResize", e.detail, userFormId);
    },
    make(modal) {
      this.$emit("makeActive", modal);
    },
    closeWindow(modal) {
      this.$emit("closeWindow", modal);
    },
    dragMouseDown(event, data) {
      event.preventDefault();
      this.refer = data;
      this.$refs.child.dragMouseDown(event);
      document.onmousemove = this.elementDrag;
      document.onmouseup = this.closeDragElement;
    },
    elementDrag: function(event) {
      event.preventDefault();
      this.$refs.child.elementDrag(
        event,
        this.$refs.outerWindowContainerRef[this.refer - 1]
      );
    },
    closeDragElement: function(event) {
      this.$refs.child.closeDragElement(event);
    },
    createTool(e, pos) {
      console.log(customLabelData);

      if (this.selectedControl == "label") {
        const tool = {
          id: this.userForms[pos - 1].controls.length + 1,
          name: "Label",
          type: "label",
          attributes: {
            value: "Good Morning"
          },
          style: {
           
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

        this.$emit("addControl", tool, pos);
      }
      if (this.selectedControl == "input") {
        console.log("kkk");
        const tool = {
          id: this.userForms[pos - 1].controls.length + 1,
          name: "Input",
          type: "input",
          attributes: {
            value: "Good Morning"
          },
          style: {
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
        console.log(tool);
        this.$emit("addControl", tool, pos);
      }
    }
  }
};
</script>




