<template>
  <div>
    <div class="left"></div>

    <div class="right">
      <div class="header">
        <button  @click="openModal()" style="display:none">Open</button>
      </div>

      <button class="addUserFormButtonStyle" @click="addUserForm()">Insert UserForm</button>

      <UserForm
        @makeActive="makeActive"
        @closeWindow="closeWindow"
        :userForms="userForms"
        :selectedControl="selectedControl"
        @addControl="addControl"
        @innerWindowResize="innerWindowResize"
      />

      <ToolBox @selectedTool="selectedTool" :prevModalZIndex="prevModalZIndex" />
    </div>
  </div>
</template>

<script>
import ToolBox from "./components/ToolBox";
import UserForm from "./components/UserForm";
import userData from "./components/JsonFiles/addUserData.json";
export default {
  name: "app",
  components: {
    ToolBox,
    UserForm
  },
  props: {
    msg: String
  },
  data() {
    return {
      userForms: userData.userForms,
      selectedControl: userData.selectedControl,
      prevModalZIndex: userData.prevModalZIndex
    };
  },
  methods: {
    innerWindowResize(e, userFormId) {
      for (let i = 0; i < this.userForms.length; i++) {
        if (this.userForms[i].id === userFormId) {
          this.userForms[i].innerWindowStyle.container.width = e.width;
          this.userForms[i].innerWindowStyle.container.height = e.height;
        }
      }
    },
    addUserForm() {
      console.log(this.userForms[0]);
      let userForm = {
        id: this.userForms.length + 1,
        name: "UserForm",
        controls: [{}],

        outerWindowStyle: {
          container: {
            position: "absolute",
            textAlign: "left",
            border: "3px solid rgb(159, 196, 224)",
            width: "600px",
            height: "400px",
            borderTopLeftRadius: "4px",
            borderTopRightRadius: "4px",
            backgroundColor: "white",
            display: "block",
            zIndex: "2"
          },

          top: {
            padding: "8px",
            background: "rgb(159, 196, 224)",
            height: "21px"
          },
          closeButton: {
            right: "10px",
            position: "absolute"
          }
        },
        innerWindowStyle: {
          container: {
            position: "absolute",
            textAlign: "left",
            border: "3px solid rgb(159, 196, 224)",
            width: "375px",
            height: "200px",
            resize: "both",
            overflow: "auto",
            borderTopLeftRadius: "4px",
            borderTopRightRadius: "4px"
          },

          top: {
            padding: "8px",
            background: "rgb(159, 196, 224)",
            height: "21px"
          },
          innerContainer: {
            width: "100%",
            height: "163px"
          },
          closeButton: {
            right: "10px",
            position: "absolute"
          }
        }
      };
      this.userForms = [...this.userForms, userForm];
    },

    addControl(tool, pos) {
      this.userForms[pos - 1].controls = [
        ...this.userForms[pos - 1].controls,
        tool
      ];
      console.log("I am tool", this.userForms[pos - 1].controls, pos, tool);
    },
    makeActive(modal) {
      console.log("Hello");
      this.previousZindex = ++this.prevModalZIndex;
      modal.outerWindowStyle.container.zIndex = this.previousZindex.toString();
    },
    openModal() {
      for (let i = 0; i < this.userForms.length; i++) {
        if (this.userForms[i].style.display === "block") {
          this.userForms[i].style.display = "none";
        } else {
          this.userForms[i].style.display = "block";
        }
      }

      this.show = !this.show;
    },
    closeWindow(modal) {
      console.log("modal of close", modal.id);
      for (let i = 0; i < this.userForms.length; i++) {
        if (this.userForms[i].id == modal.id) {
          console.log(this.userForms[i]);
          this.userForms[i].outerWindowStyle.container.display = "none";
        }
      }
    },
    selectedTool(tool) {
      console.log(this.selectedControl);
      this.selectedControl = tool;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  padding: 22px;
  text-align: center;
  background: #80888e;
  color: black;
  font-size: 22px;
  margin-top: -20px;
}

.left {
  left: 0;
  height: 100%;
  width: 30%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
}

.right {
  right: 0;
  background-color: #e3e3e3;
  height: 100%;
  width: 70%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
}
.addUserFormButtonStyle
{
  
    position: absolute;
    top: 7px;
    margin: 0px;
    padding: 5px;

}
</style>
