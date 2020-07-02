<template>
  <div>
    <div class="container">
      <div class="top  w-frame">
        <div class="closeButton">
          <div class="ui-titlecontrols">
            <button class="ui-btn minimize">
              <svg x="0px" y="0px" viewBox="0 0 10.2 1">
                  <rect x="0" y="50%" width="10.2" height="1" />
              </svg>
            </button>
            <button class="ui-btn maximize">
              <svg viewBox="0 0 10 10" >
                <path d="M0,0v10h10V0H0z M9,9H1V1h8V9z" />
              </svg>
            </button>
            <button class="ui-btn close">
              <svg viewBox="0 0 10 10">
                <polygon
                  points="10.2,0.7 9.5,0 5.1,4.4 0.7,0 0,0.7 4.4,5.1 0,9.5 0.7,10.2 5.1,5.8 9.5,10.2 10.2,9.5 5.8,5.1"
                />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "windowView"
};
</script>

<style  scoped>

.container {
  position: absolute;
  text-align: left;
  border: 3px solid #9cb7d4;
  width: 200px;
  height: 400px;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  background-color: white;
  display: block;
  z-index: 2;
}
.btn {
}
.top {
  padding: 8px;
  height: 21px;
  background:-webkit-linear-gradient(30deg,#adc9e7ba 0%,#6e8ab1 50%,#768bb7 51%,#a1bdd28f 100%); 
  background:-moz-linear-gradient(30deg,#225283 0%,#6A92B6 50%,#5B8EB9 51%,#225283 100%); 
  background:-ms-linear-gradient(30deg,#225283 0%,#6A92B6 50%,#5B8EB9 51%,#225283 100%); 
  background:-o-linear-gradient(30deg,#225283 0%,#6A92B6 50%,#5B8EB9 51%,#225283 100%); 
  background:linear-gradient(30deg,#adc9e7ba 0%,#7f99bd 50%,#8398c6 51%,#a1bdd28f 100%) 
}
.closeButton {
  right: 10px;
  position: absolute;
}

#button-wrap {
  float: right;
}
.ui-titlecontrols {
  max-width: 144px;
  max-height: 32px;
  flex-grow: 1;
}
.ui-btn {
  margin: 2px;
  background: transparent;
}
.ui-btn:hover {
  background: rgba(255, 255, 255, 0.1);
}
.ui-btn.close:hover {
  background: #e81123;
}
.ui-btn svg path,
.ui-btn svg rect,
.ui-btn svg polygon {
  fill: white;
}
.ui-btn svg {
  width: 10px;
  height: 10px;
  stroke: white;
  stroke-width: 2px;
}
.w-frame { 
 /*  width:800px; 
  border:1px solid rgba(0,0,0,0.8); 
 
  position:absolute; 
  top:50%; 
  left:50%; 
  margin:-200px 0px 0px -400px; 
  -webkit-border-radius:7px; 
  -moz-border-radius:7px; 
  border-radius:7px; 
  -webkit-box-shadow:0px 1px 5px #000,0px 0px 10px rgba(0,0,0,0.5); 
  -moz-box-shadow:0px 1px 5px #000,0px 0px 10px rgba(0,0,0,0.5); 
  box-shadow:0px 1px 5px #000,0px 0px 10px rgba(0,0,0,0.5);  */
}
</style>