<template>
  <div>
    <div class="left"></div>

   <!--  <div class="right"></div> -->

    <div class="right">
      <div class="header">
        <button @click="openModal()" style="display:none">Open</button>
      </div>

      <button @click="addUserForm()">Insert UserForm</button>

      <UserForm
        @makeActive="makeActive"
        @closeWindow="closeWindow"
        :modals="modals"
        :selected="selected"
        @addControl="addControl"
      />

      <ToolBox @selectedTool="selectedTool"  />

     <!--  <div style="height: 500px; width: 500px; border: 1px solid red; position: absolute;">
        
          <vue-draggable-resizable
            :w="100"
            :h="200"
            :x="20"
            :y="20"
            :parent="true"
            :debug="true"
            @resizing="onResize"
           
          >
            
            <p :style="v">jjj</p>
          </vue-draggable-resizable>
       
      </div> -->
    </div>
  </div>
</template>

<script>
import ToolBox from "./components/ToolBox";
import UserForm from "./components/UserForm";
/* import VueDraggableResizable from "./components/vue-draggable-resizable"; */
export default {
  name: "app",
  components: {
    ToolBox,
    UserForm,
   /*  VueDraggableResizable */
  },
  props: {
    msg: String
  },
  data() {
    return {
      selected: "hhhhh",

       v:
       {
         width:"100px",
         height:"200px",
         border:"1px solid",
         position:"absolute",
         left:20,
         top:20
        
       },
      prevModalZIndex: 2,
      modals: [
        {
          id: 1,
          name: "UserForm",
          selected: "label",
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
                left: "50",
                top: "54",
                width: "100",
                height: "40",
                resize: "both",
                overflow: "auto",
                zIndex: "1",
                border: "1px solid"
              }
            }
          ],

          style: {
            position: "absolute",
            display: "none",
            zIndex: 1,
            borderTop: "40px solid skyblue",
            borderLeft: "13px solid skyblue",
            borderRight: "13px solid skyblue",
            borderBottom: "13px solid skyblue",
            paddingTop: "5px",
            paddingLeft: "5px",
            width: "400px",
            height: "500px",
            background: "white",
            borderRadius: "1%",
            top: "10px",
            left: "20px"
          },
          inner: {
            borderTop: "40px solid skyblue",
            borderLeft: "10px solid skyblue",
            borderRight: "10px solid skyblue",
            borderBottom: "10px solid skyblue",
            borderRadius: "1%",
            width: "250px",
            height: "300px",
            top: "0px",
            left: 0,
            background: "#fff",
            marginTop: "5px",
            marginLeft: "5px",
            resize: "both",
            overflow: " auto"
          },
          headerText: {
            marginTop: "-35px",
            marginLeft: "-11px",
            position: "absolute"
          },
          innerHeaderText: {
            top: "4px",
            position: "absolute !important"
          },
          closeButton: {
            position: " absolute",
            right: "-208px"
          },
          closeInnerButton: {
            position: "absolute",
            right: "-174px"
          }
        },
        {
          id: 2,
          name: "UserForm",
          controls: [
            {
              id: "",
              name: "",
              type: "input",
              attributes: {},
              style: {}
            },
            {
              id: 2,
              name: "Label",
              type: "label",
              caption: "Text for label",
              style: {
                top: "10px",
                left: "20px",
                width: "200px",
                height: "150px"
              },
              attributes: {
                name: "",
                value: ""
              }
            }
          ],
          style: {
            position: "fixed",
            display: "none",
            zIndex: 1,
            borderTop: "40px solid skyblue",
            borderLeft: "13px solid skyblue",
            borderRight: "13px solid skyblue",
            borderBottom: "13px solid skyblue",
            paddingTop: "5px",
            paddingLeft: "10px",
            width: "400px",
            height: "500px",
            background: "red",
            borderRadius: "1%"
          },
          inner: {
            borderTop: "40px solid skyblue",
            borderLeft: "10px solid skyblue",
            borderRight: "10px solid skyblue",
            borderBottom: "10px solid skyblue",
            borderRadius: "1%",
            width: "250px",
            height: "300px",
            top: "0px",
            left: 0,
            position: "absolute",
            background: "#fff",
            marginTop: "5px",
            marginLeft: "5px",
            resize: "both",
            overflow: " auto"
          },
          headerText: {
            marginTop: "-35px",
            marginLeft: "-11px",
            position: "absolute"
          },
          innerHeaderText: {
            marginTop: "-35px",
            marginLeft: "-200px",
            position: "absolute"
          },
          closeButton: {
            position: " absolute",
            right: "-208px"
          },
          closeInnerButton: {
            position: "absolute",
            right: "-174px"
          }
        }
      ],
      show: false
    };
  },
  methods: {
    onResize: function(x, y, width, height) {
      console.log("jjjjjjjjjjj",x, y, width, height);
    },
    addUserForm() {
      let userForm = {
        id: this.modals.length + 1,
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

        style: {
          position: "fixed",
          display: "block",
          zIndex: ++this.prevModalZIndex,
          borderTop: "40px solid #e1eaf1",
          borderLeft: "10px solid #e1eaf1",
          borderRight: "10px solid #e1eaf1",
          borderBottom: "10px solid #e1eaf1",
          paddingTop: "5px",
          paddingLeft: "10px",
          width: "600px",
          height: "400px",
          background: "white",
          borderRadius: "1%"
        },
        inner: {
          borderTop: "40px solid #e1eaf1",
          borderLeft: "8px solid #e1eaf1",
          borderRight: "8px solid #e1eaf1",
          borderBottom: "8px solid #e1eaf1",
          borderRadius: "1%",
          width: "375px",
          height: "200px",
          top: "0px",
          left: 0,
          background: "#fff",
          marginTop: "1px",
          marginLeft: "1px",
          resize: "both",
          overflow: " auto"
        },
        headerText: {
          marginTop: "-35px",
          marginLeft: "-11px",
          position: "absolute"
        },
        innerHeaderText: {
          top: "4px",
          position: "absolute !important"
        },
        closeButton: {
          position: " absolute",
          right: "-403px"
        },
        closeInnerButton: {
          position: "absolute",
          right: "-300px"
        }
      };
      this.modals = [...this.modals, userForm];
    },

    addControl(tool, pos) {
      this.modals[pos - 1].controls = [...this.modals[pos - 1].controls, tool];
      console.log("I am tool", this.modals[pos - 1].controls, pos, tool);
    },
    makeActive(modal) {
      console.log("Hello");
      this.previousZindex = ++this.prevModalZIndex;
      modal.style.zIndex = this.previousZindex.toString();
    },
    openModal() {
      for (let i = 0; i < this.modals.length; i++) {
        if (this.modals[i].style.display === "block") {
          this.modals[i].style.display = "none";
        } else {
          this.modals[i].style.display = "block";
        }
      }

      this.show = !this.show;
    },
    closeWindow(modal) {
      console.log("modal of close", modal.id);
      for (let i = 0; i < this.modals.length; i++) {
        if (this.modals[i].id == modal.id) {
          console.log(this.modals[i]);
          this.modals[i].style.display = "none";
        }
      }
    },
    selectedTool(tool) {
      console.log(this.selected);
      this.selected = tool;
    },

    getPos(e) {
      // var rect = e.target.getBoundingClientRect();
      // console.log(e.clientX - rect.left);
      // console.log(e.clientY - rect.top);

      // console.log("===============");
      // console.log(this.$refs.pos.getBoundingClientRect().left);
      // console.log(this.$refs.pos.getBoundingClientRect().top);

      console.log("===============");
      console.log(e.offsetX); // will get left
      console.log(e.offsetY); // will get top
      console.log("===============");
    },
    first() {
      console.log("First Clicked");
    },
    second() {
      console.log("Second Clicked");
    }
    // created() {
    //   this.prevModalZIndex = this.modals[this.modals.length - 1].style.zIndex;
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
  background-color: transparent;
  border: none;
  color: white;
}
.header {
  padding: 22px;
  text-align: center;
  background: #366f9a;
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
  background-color: dimgrey;
  height: 100%;
  width: 70%;
  position: fixed;
  z-index: 1;
  top: 0;
  overflow-x: hidden;
  padding-top: 20px;
}
</style>
