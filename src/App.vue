<template>
  <div>
    <div class="left">
     
    </div>

    <div class="right" >
      <div class="header">
        <button @click="openModal()" style="display:none">Open</button>
      </div>

      <button @click="addUserForm()">Insert UserForm</button>

      <UserForm
        @makeActive="makeActive"
        @closeWindow="closeWindow"
        :userForms="userForms"
        :selectedControl="selectedControl"
        @addControl="addControl"
      />

      <ToolBox   @selectedTool="selectedTool" :prevModalZIndex="prevModalZIndex" />

      <!-- <div style="height: 500px; width: 500px; border: 1px solid red; position: absolute;">
        
          <vue-draggable-resizable
            :w="parseInt(v.width)"
            :h="parseInt(v.height)"
            :x="parseInt(v.left)"
            :y="parseInt(v.top)"
            :parent="true"
            :debug="false"
            @resizing="onResize"
           
          >
            
            <span :style="v">jjj</span>
          </vue-draggable-resizable>
       
      </div>-->
    </div>
  </div>
</template>

<script>
import ToolBox from "./components/ToolBox";
import UserForm from "./components/UserForm";


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
      selectedControl: "",
      v: {
        width: "50px",
        height: "20px",
        border: "1px solid",
        position: "absolute",
        left: "0px",
        top: "0px"
      },
      prevModalZIndex: 2,
      userForms: [
        {
          id: 1,
          name: "UserForm",
          controls: [
            {
              id: 1,
              name: "Label",
              type: "label",
              attributes: {
                value: "Good Morning"
              },
              style: {
                position: "absolute",
                left: "50px",
                top: "54px",
                width: "100px",
                height: "40px",
                resize: "both",
                overflow: "auto",
                zIndex: "1",
                border: "1px solid"
              }
            }
          ],

          outerWindowStyle: {
            container: {
              position: "absolute",
              textAlign: "left",
              border: "3px solid rgb(159, 196, 224)",
              width: "600px",
              height: "400px",
              borderTopLeftRadius: "4px",
              borderTopRightRadius: "4px",
              backgroundColor:"white",
              display:"block",
              zIndex:"2"
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
            innerContainer:
            {
                width:"100%",
                height:"163px"
            },
            closeButton: {
              right: "10px",
              position: "absolute"
            }
          }
        }
        
      ],
      show: false
    };
  },
  methods: {
    onResize: function(x, y, width, height) {
      console.log("jjjjjjjjjjj", x, y, width, height);
      console.log(this.v.left, this.v.top, this.v.width, this.v.height);
      (this.v.width = `${width}px`),
        (this.v.height = `${height}px`),
        (this.v.left = `${x}px`),
        (this.v.top = `${y}px`);
    },
    addUserForm() {
      let userForm = {
        id: this.userForms.length + 1,
        name: "UserForm",
        controls: [
          {
            /* id: 1,
            name: "Label",
            type: "label",
            caption: "Text for label",
            style: {
              top: "10px",
              left: "20px",
              width: "200px",
              height: "150px",
              border:"1px solid"
            },
            attributes: {
              name: "",
              value: ""
            } */
          }
        ],

        
          outerWindowStyle: {
            container: {
              position: "absolute",
              textAlign: "left",
              border: "3px solid rgb(159, 196, 224)",
              width: "600px",
              height: "400px",
              borderTopLeftRadius: "4px",
              borderTopRightRadius: "4px",
              backgroundColor:"white",
              display:"block",
              zIndex:"2"
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
            innerContainer:
            {
                width:"100%",
                height:"163px"
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
      this.userForms[pos - 1].controls = [...this.userForms[pos - 1].controls, tool];
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
    },

   
    // created() {
    //   this.prevModalZIndex = this.userForms[this.userForms.length - 1].style.zIndex;
    // }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.outer1 {
  overflow: auto;
  position: absolute;
  display: none;
  z-index: 1;
  border-top: 40px solid skyblue;
  border-left: 13px solid skyblue;
  border-right: 13px solid skyblue;
  border-bottom: 13px solid skyblue;
  padding-top: 5px;
  padding-left: 5px;
  width: 400px;
  height: 500px;
  background: white;
  border-radius: 1%;
}
.inner {
  border-top: 40px solid skyblue;
  border-left: 10px solid skyblue;
  border-right: 10px solid skyblue;
  border-bottom: 10px solid skyblue;
  border-radius: 1%;
  width: 250px;
  height: 300px;
  top: 0px;
  left: 0;
  position: absolute;
  background: #fff;
  margin-top: 5px;
  margin-left: 5px;
  resize: both;
  overflow: auto;
}
.first {
  position: absolute;
  left: 20px;
  top: 10px;
  width: 100px;
  height: 40px;
  resize: both;
  overflow: auto;
}
.second {
  position: absolute;
  left: 100px;
  top: 100px;
  resize: both;
  overflow: auto;
}
.third {
  position: absolute;
  left: 100px;
  top: 150px;
  resize: both;
  overflow: auto;
}
.headerText {
  margin-top: -35px;
  margin-left: -11px;
  position: absolute;
}
.innerHeaderText {
  margin-top: -35px;
  margin-left: -200px;
}
.closeButton {
  position: absolute;
  top: 10px;
  right: 10px;
}
.closeInnerButton {
  position: absolute;
  right: 10px;
}
button {
  margin-top: -38px;
  position: absolute;
  padding: 5px;
  /* background-color: transparent; */
  border: none;
  color: black;
  margin-left: 12px;
}
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
</style>
