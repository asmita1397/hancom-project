<template>
  <div id="container">
    <!--  <ParentWindow /> -->

    <div class="modal-vue">
      <!--   <button @click="openModel(true)" style="display:none">show</button> -->

      <!-- overlay -->
      <div class="overlay" v-if="showModal" @click="openModel(false)"></div>

      <!-- modal -->
      <div class="modal" v-if="showModal" >
        <div class="top">
          <span>ChildWindow{{this.name}}</span>
          <button class="close" disabled>x</button>
        </div>
        <div class="modal-container" ref="container1" @click="childClick($event)">
          <!--   <p>jjjjj</p> -->
        </div>
        <Label style="display:none" />
      </div>
    </div>
  </div>
</template>

<script>
/* import ParentWindow from "./ParentWindow"; */
import Label from "./Label";
import Vue from "vue";
export default {
  name: "App",
  components: {
    Label
  },
  props: {
    show: Boolean,
    name: Number
  },
  data() {
    return { showModal: true };
  },
  methods: {
    openModel(data) {
      console.log("data", data);
      this.showModal = data;
    },
    childClick(e) {
      console.log("hhhhhh", e.offsetX);
      console.log("hhhhhh", e.offsetY);

      var ComponentClass = Vue.extend(Label);
      var instance = new ComponentClass({
        propsData: { text: "nnnnn" }
      });
      instance.$mount(); // pass nothing
      /*  this.$refs.container1.appendChild(instance.$el).style.left = e.offsetX */
      this.$refs.container1.appendChild(instance.$el).style.top = `${e.offsetY}px`;
      this.$refs.container1.appendChild(instance.$el).style.left = `${e.offsetX}px`;
      
    }
  }
};
</script>

<style scoped>
/* .modal-vue .overlay {
  position: fixed;
  z-index: 9998;
  top: 56px;
  left: 112px;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
} */

.modal-vue .modal {
  position: fixed;
  width: 500px;
  margin: 10px 10px;
  background-color: #fff;
  border: 5px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-style: solid;
  height: 300px;
}
.modal-container {
  position:fixed;
  width: 495px;
  border: 5px solid #f1f1f1;
  border-style: solid;
  height: 255px;
  background-color:white;
  
}

.modal-vue .close {
  position: absolute;
  top: 10px;
  right: 10px;
}
.top {
  position: relative;
  top: 0;
  left: 0;
  padding: 10px;
  background: #f1f1f1;
}
</style>

