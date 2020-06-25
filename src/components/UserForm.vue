<template>
  <div id="container" >
    
    <br />
    <div class="modal-vue">
      <!--   <button @click="openModel(true)" style="display:none">show</button> -->

      <!-- overlay -->
      <div class="overlay" v-if="showModal" @click="openModel(false)"></div>

      <!-- modal -->
      <div class="modal" v-if="showModal">
        <div class="top">
          <span> UserForm {{this.name}}</span>
          <button class="close" @click="openModel(false)">x</button>
        </div>
          
            <ChildWindow  :show="this.show" :name="this.name" />
      </div>
    </div>
 
  </div>
</template>

<script>
import ChildWindow from "./ChildWindow";

export default {
  name: "UserForm",
  components: {
    ChildWindow,
    
  },
  props:{
        show:String,
        name:Number
  },
  data() {
    return { showModal: this.show };
  },
  methods: {
    openModel(data) {
      console.log("data", data);
      this.showModal = data;
    },
    handleChild()
    {
      console.log("child component clicked")
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
  width: 80%;
  z-index: 50%;
  margin: 0 auto;
  background-color: #fff;
  border: 5px solid #f1f1f1;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  border-style: solid;
  height: 400px;
}

.modal-vue .close {
  position: absolute;
  top: 10px;
  right: 10px;
  
}
.top {
  position: relative;
  top:0;
  left:0;
  padding: 20px;
  background: #f1f1f1;
 
}
</style>

