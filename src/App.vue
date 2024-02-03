
<template>

  <container>
    <div class="maker">
      <Builder></Builder>
    </div>

  </container>



  <!--img alt="Vue logo" src="./assets/logo.png"-->



</template>

<script>

import Builder from './components/Builder.vue'
// import SaveLoad from './components/SaveLoad.vue'
// import html2canvas from 'html2canvas';

export default 
{
  name: 'App',
  components: 
  {
    Builder
  },
  methods:
  {

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
