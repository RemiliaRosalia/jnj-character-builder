
<template>
  <!--button @click="takeScreenshot">Take Screenshot</button-->
  <container>
    <div id="capture" class="maker">
      <Builder></Builder>
    </div>

  </container>



  <!--img alt="Vue logo" src="./assets/logo.png"-->



</template>

<script>

import Builder from './components/Builder.vue'
import SaveLoad from './components/SaveLoad.vue'
import html2canvas from 'html2canvas';

export default 
{
  name: 'App',
  components: 
  {
    Builder,
    SaveLoad
  },
  methods:
  {
    takeScreenshot()
    {
      html2canvas(document.querySelector("#capture")).then(canvas => 
      {
        document.body.appendChild(canvas)
        // const dataURI = "data:text/plain;base64," + encodeBase64(
        //    this.name + ','+this.race + ',' + this.title + ',' + this.imgURL + ' ,' + this.primColor + ',' + this.secColor + ',' + this.allignment + ',' + this.skill + ',' + this.ability
        //    + ',' + this.abilityDesc + ',' + this.isOneshot + ',' + this.level + ',' + this.statTotal + ',' + this.stats);
        //saveAs(canvas, "test.png");
      });


    }
  }
}

</script>


<style>
#app 
{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.maker
{
  width:100%;
  height:10%;
 
  /* background: hsl(289, 100%, 93%) */
}
.preview
{
width: 50%;
float: right;

}

</style>
