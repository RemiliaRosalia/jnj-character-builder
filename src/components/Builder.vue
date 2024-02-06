<template>
  <div></div>
    <button @click="saveFile">Save Character</button>
  <input id="fileInput" type="file" ref="doc" style="display:none;" @change="loadFile"/>
  <button onclick="document.getElementById('fileInput').click();">Load Character</button>
  <br>
  <!-- <button @click="takeScreenshot">Take Screenshot</button>
  <br> -->
  <div class="builder" id="capture">
    <!--Base Info-->
  <label class="header">
  <input type="text" v-model="name" class="secondary">
  <button @click="levelUp(-1)" v-show="buttonsOn"  :disabled="isOneshot" class="levelButton">-</button>
    Level: {{ level }}
    <button @click="levelUp(1)" v-show="buttonsOn"  :disabled="isOneshot" class="levelButton">+</button>
</label>
<div class="body"></div>
  <!--IMAGE-->

  <img src='' class="portrait" width="100px" height="100px">
  <div class="bio">
    <label>Race: 
    <input type="text" v-model="race" class="primary"></label>
    <br>
    <br>
    <label>Title: 
    <input type="text" v-model="title" class="primary"></label>
    <br>
    <br>
    <label> Skill: 
    <input type="text" v-model="skill"  class="primary"></label>
  </div>
  <div class="sidebar">
  <div class="sidestats">  
    <label>{{ hp }}hp</label>
    <br>
    <br>
    <label>{{ mp }}mp</label>
    <br>
    <br>
    <label style="font-size: 60px;" v-show="statPoints!=0">{{ statPoints }} points</label>
  </div>
  <div class="alignment" @change="alignmentChanged()">
      <div class="LG" onclick="document.getElementById('LG').click();"><input id="LG" type="radio" name='moral' value="LG" v-model="alignment"></div>
      <div class="NG" onclick="document.getElementById('NG').click();"><input id="NG" type="radio" name='moral' value="NG" v-model="alignment"></div>
      <div class="CG" onclick="document.getElementById('CG').click();"><input id="CG" type="radio" name='moral' value="CG" v-model="alignment"></div>
      <div class="LN" onclick="document.getElementById('LN').click();"><input id="LN" type="radio" name='moral' value="LN" v-model="alignment"></div>
      <div class="NN active" onclick="document.getElementById('NN').click();"><input id="NN" type="radio" name='moral' value="NN" v-model="alignment"></div>
      <div class="CN" onclick="document.getElementById('CN').click();"><input id="CN" type="radio" name='moral' value="CN" v-model="alignment"></div>
      <div class="LE" onclick="document.getElementById('LE').click();"><input id="LE" type="radio" name='moral' value="LE" v-model="alignment"></div>
      <div class="NE" onclick="document.getElementById('NE').click();"><input id="NE" type="radio" name='moral' value="NE" v-model="alignment"></div>
      <div class="CE" onclick="document.getElementById('CE').click();"><input id="CE" type="radio" name='moral' value="CE" v-model="alignment"></div>
    </div>
  </div>
  <div class="stats">
    <label>END:
    <button @click="changeStat(0,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[0]">
    <button @click="changeStat(0,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>WIS:
    <button @click="changeStat(3,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[3]">
    <button @click="changeStat(3,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>CHR:
    <button @click="changeStat(6,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[6]">
    <button @click="changeStat(6,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>MYS:
    <button @click="changeStat(1,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[1]">
    <button @click="changeStat(1,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>DEX:
    <button @click="changeStat(4,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[4]">
    <button @click="changeStat(4,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>LCK:
    <button @click="changeStat(7,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[7]">
    <button @click="changeStat(7,1)" v-if="buttonsOn" class="statButton">+</button></label>

    <label>STR:
    <button @click="changeStat(2,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[2]">
    <button @click="changeStat(2,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label>PER:
    <button @click="changeStat(5,-1)" v-if="buttonsOn" class="statButton">-</button>
    <input type="number" v-model="stats[5]">
    <button @click="changeStat(5,1)" v-if="buttonsOn" class="statButton">+</button></label>
    <label v-show="!isNPC">PRS:
    <button @click="changeStat(8,-1)" v-if="buttonsOn"  class="statButton">-</button>
    <input type="number" v-model="stats[8]">
    <button @click="changeStat(8,1)" v-if="buttonsOn" class="statButton">+</button></label>
  </div>
    <div class="footer">
  <label><input type="text" v-model="ability" class="ability"></label>
  <br>
  <label></label>
  <textarea name="paragraph_text" cols="65" rows="6" v-model="abilityDesc" class="ability"></textarea>
</div>


</div>

  <br>
  <label>
  <input type="text" v-model="imgURL" @click="changeImg"/></label>
  <br>
  <!--COLOR PICKERS-->
  <input type="color" v-model="primColor" @change="shadeSet(true)">
  <input type="color" v-model="secColor" @change="shadeSet(false)">
  <br>
  <label>Select Alignment: </label>
    <br>

<br>


  <label>Is oneshot: {{ isOneshot }}
    <!-- !isOneshot since value does not update before the function-->
  <input type="checkbox"  v-model="isOneshot" @click="oneshotLevelSwitch(!isOneshot)"></label>
  
  <br>
  <label>Is NPC: {{ isNPC }}
  <input type="checkbox"  v-model="isNPC" @click="npcLevelSwitch(!isNPC)"></label>
  <br>
  <button @click="buttonsOn=!buttonsOn">Toggle Buttons</button>
  <label>{{ buttonsOn }}</label>
<!--Stat Building-->
<p>You are level {{ level }} and have {{ statPoints }} / {{statTotal}} points left.</p>
<button @click="levelUp(-1)" :disabled="isOneshot">LEVEL DOWN</button>
<button @click="levelUp(1)" :disabled="isOneshot">LEVEL UP</button>
<br>
<br>


</template>

<script>
import { watch, ref } from 'vue'
import { saveAs } from 'file-saver';
import html2canvas from 'html2canvas';

const reader = new FileReader();

export default 
{
  //Official Character Sheet sizes
  //Picture: 329 x 239
  //Full Sheet: 1210 x 904
    data()
    {
        return{
            name: 'YourName',
            race: 'YourRace',
            title: 'YourTitle',
            imgURL: 'Type IMG url here',
            //primColor: rgb(153, 34, 34),
            primColor: "#992222",
            primShade: "#800909",
            //secColor: rgb(188, 188, 188),
            secColor: "#bcbcbc",
            secShadeL: "#eeeeee",
            secShadeD: "#a3a3a3",
            alignment: 'NN',
            skill: 'YourSkill',
            ability: 'AbilityName',
            abilityDesc: 'Please type the description',
            isOneshot: false,
            isNPC: false,
            level: 1,
            statTotal: 35,
            statPoints: 22,
            //Stats
            stats: [1,1,1,1,1,1,1,1,5],
            hp: 11,
            mp: 1,
            inputText: '',
            inputArray: [],
            buttonsOn: true
        }
    },
    methods:
    {
      changeImg()
      {
        console.log("code attempted")
        var image = document.getElementsByClassName("portrait")[0]
        console.log(image)
        image.src = this.imgURL;
      },
      //Sets curent alignment to have full opacity
      alignmentChanged()
      {
        //document.getElementById("MyElement").classList.add('MyClass');
        document.getElementsByClassName("active")[0].classList.remove("active");
        document.getElementsByClassName(this.alignment)[0].classList.add("active");
      },
      shadeGenerate(c,v)
      {
        //c is color, v is value
        let aRGBHex=c.slice(1, 7).match(/.{1,2}/g);
        let aRGB = 
        [    
          parseInt(aRGBHex[0], 16),
          parseInt(aRGBHex[1], 16),
          parseInt(aRGBHex[2], 16)
        ]
        for(let i=0;i<aRGB.length;i++)
        {
          //console.log("hi " + aRGB[i])
          aRGB[i]=Math.trunc(aRGB[i] + v);
          if(aRGB[i]>255)
            aRGB[i]=255;
          //console.log("bye " + aRGB[i])
        }
        return("#" + ((1 << 24) + (aRGB[0] << 16) + (aRGB[1] << 8) + aRGB[2]).toString(16).slice(1));
       //console.log(aRGB);
      },
      shadeSet(isPrime)
      {
        if(isPrime)
        {
          this.primShade = this.shadeGenerate(this.primColor,-25)
          console.log(this.primShade)
        }
        else
        {
          this.secShadeD = this.shadeGenerate(this.secColor,-25);
          console.log(this.secShadeD)
          this.secShadeL = this.shadeGenerate(this.secColor,50)
          console.log(this.secShadeL)
        }
      },
      oneshotLevelSwitch(x)
      {
        if(x)
        {
          //console.log("YES");
          this.level = 3;
          this.statTotal = 40;
          this.calculateTotal()
        }
        else
        {
          //console.log("NO");
          this.level = 1;
          this.statTotal = 35;
          this.calculateTotal()
        }
      },
      npcLevelSwitch(x)
      {
        if(x)
        {
          //console.log("YES");
          this.statTotal = this.level*5 +25;
          this.calculateTotal()
        }
        else
        {
          //console.log("NO");
          this.level = 1;
          this.statTotal = 35;
          this.calculateTotal()
        }
      },
      levelUp(x)
      {
        this.level += x;
        if(this.level<=0)
        {
          this.level=1;
        }
        if(this.isOneshot)
        {
          this.statTotal=40;
          this.level= 3;
        }
        else if(this.isNPC)
        {
          this.statTotal = 25 + this.level *5;
        }
        else if(this.level<=5)
        {
          this.statTotal= 32 + this.level*3;
        }
        else
        {
          this.statTotal = 47 + (this.level - 5)
        }

        this.calculateTotal()
      },
      changeStat(stat, value)
      {
              this.stats[stat] = this.stats[stat] + value;
              this.calculateTotal()
      },
      calculateTotal()
      {
        let x = this.statTotal
        //console.log("stat total is" + this.statTotal)
        for(let i=0; i<this.stats.length;i++)
        {
          //ifs make sure stats are between 1 and 8
          //will need to implement specifics if stats can be uncapped
          if(!this.isNPC)
          {
            if(this.stats[i]>8)
            {
              this.stats[i]=8;
            }
            else if(this.stats[i]<1)
            {
              this.stats[i]=1;
            }
            else if(this.stats[8]<5)
            {
              this.stats[8]=5;
            }
            x-= this.stats[i];
          }
          else if (i!=8)
          {
            //console.log("Hi im an npc and this stat is number " + i)
            x-=this.stats[i]
          }

        } 
        this.statPoints = x;
        this.hp =Math.trunc(10+ this.stats[0] * (.5 * Math.min(this.level, 5) + .5));
        this.mp =Math.trunc(this.stats[1] * (.25 * Math.min(this.level, 5) + .75));
      },
      saveFile()
        {
          //console.log(this.stats)
          // name(0), race(1), title(2), imgURL(3), primColor(4), secColor(5), alignment(6), skill(7), ability(8), abilityDesc(9), Oneshot(10), NPC(11), level, stats
          var FileSaver = require('file-saver');
          var blob = new Blob([this.name + '√'+this.race + '√' + this.title + '√' + this.imgURL + ' √' + this.primColor + '√' + this.secColor + '√' + this.alignment + '√' + 
          this.skill + '√' + this.ability + '√' + this.abilityDesc + '√' + this.isOneshot + '√' + this.isNPC + '√' + this.level + '√'+ this.stats[0] + '√'+ this.stats[1] + '√'+ this.stats[2] + 
          '√'+ this.stats[3] + '√'+ this.stats[4] + '√'+ this.stats[5] + '√'+ this.stats[6] + '√'+ this.stats[7] + '√'+ this.stats[8]], 
          {type: "text/plain;charset=utf-8"});
          FileSaver.saveAs(blob, this.name + ".txt");
        },

      loadFile()
        {
          this.isNPC= false;
          this.isOneshot = false;
          this.file = this.$refs.doc.files[0];
          if (this.file.name.includes(".txt")) 
          {
            //console.log("file is a .txt")
            reader.onload = (res) => 
            {
              //sets inputText to the file's info
              this.inputText = res.target.result;
              this.convertFile();
            };
            reader.onerror = (err) => console.log(err);
            reader.readAsText(this.file);
          } 
          else 
          {
            this.inputText = "check the console for file output";
            reader.onload = (res) => 
            {
              console.log(res.target.result);
            };
            reader.onerror = (err) => console.log(err);
            reader.readAsText(this.file);
          }
        },
        convertFile()
        {
          console.log(this.inputText)
          this.inputArray = this.inputText.split("√")
          //let x= Number(this.inputArray[20]) + 5
          this.name=this.inputArray[0];
          this.race=this.inputArray[1];
          this.title=this.inputArray[2];
          this.imgURL=this.inputArray[3];
          this.primColor=this.inputArray[4];
          this.secColor=this.inputArray[5];
          this.alignment=this.inputArray[6];
          this.skill=this.inputArray[7];
          this.ability=this.inputArray[8];
          this.abilityDesc=this.inputArray[9];
          /*ok what the frick was this?
          SO THE ISSUE I HAD WAS BECAUSE OF SOME STRING VS BOOLEON BS????
          THIS IS WHY I HATE JAVASCRIPT HAVING NO TYPE DECLARATIONS UGH
          I STILL HAVE NO EXACT IDEA HOW IT HAPPENED?
          I THINK BECAUSE ANY STRING VALUE THAT ISNT NULL IS TRUE WHICH INCLUDES "false" BEING TRUE???????????
          */
          if(this.inputArray[10]=="true")
          {
            this.isOneshot=true;
          }
          if(this.inputArray[11]=="true")
          {
            this.isNPC=true;
          }

          this.level=Number(this.inputArray[12]);
          for(let i=0; i<this.stats.length;i++)
          {
            this.stats[i]=Number(this.inputArray[i+13])
          }
          this.calculateTotal()
          this.changeImg()
          this.alignmentChanged()
          this.shadeSet(true);
          this.shadeSet(false);
          this.levelUp(0);
        },
        takeScreenshot()
        {
          html2canvas(document.querySelector("#capture")).then(canvas => 
          {
            document.body.appendChild(canvas)
          });
        }
    }
}

</script>
<link href='https://fonts.googleapis.com/css?family=Gabriela' rel='stylesheet'></link>
<style>
.builder
{
  background: v-bind('primColor');
  color: black;
  /* font-family: Gabriola; */
  font-family: 'Gabriela';
  font-size: 50px;
  display:grid;
  grid-template-areas:
    'header header header header header sidebar'
    'portrait main main main main sidebar'
    'stats stats stats stats stats sidebar'
    'footer footer footer footer footer sidebar';

  width: 1210px;
  height: 878px;
  /* align-content: center; */
  float:left;
  
}
.statButton
{
  height:75%;
  width:10%;
  font-size: 25px;
}
.levelButton
{
  height:75%;
  width:7%;
  font-size: 25px;
}
.header
{
  grid-area: header;
  background: v-bind('secColor');
}
.portrait
{
  grid-area: portrait;
    border: 7px solid v-bind('secShadeL');
  width: 300px;
  height: 300px;
}
.bio
{
  grid-area: main;
  
}
.stats
{
  grid-area: stats;
  display: inline-grid;
  grid-template-columns: auto auto auto;
  align-content: center;
  font-weight: bold;
}
.sidebar
{
  font-size: 100px;
  grid-area: sidebar;
  width:285px;
  /* height:100px; */

}
.sidestats
{
  border: 7px solid v-bind('secShadeD');
  background: v-bind('primShade');
  width:271px;
  /* height:500px; */
  height: 579px;
}
.footer
{
  grid-area: footer;
  background: v-bind('primShade');
  border: 7px solid v-bind('secShadeD');
  align-content: bottom;
  height: 98%
}
input[type="number"]
{
width:15%;
height:100%;
text-align: center;
-webkit-appearance: textfield;
-moz-appearance: textfield;
appearance: textfield;
font-family: 'Gabriela';
  font-size: 50px;
  background: v-bind('primColor');
  border:none;
  font-weight: bold;
}
input[type="text"]
{
  font-family: 'Gabriela';
  font-size: 50px;
  border:none;
}
input[type="radio"]
{
  /* margin-left: 10px;
  margin-right: 10px; */
  /* width:25px;
  height:25px; */
  background:blueviolet;
  display: none; 
}
textarea
{
  font-family: 'Gabriela';
  font-size: 25px;
}
.ability
{
  background: v-bind('primShade');
  border: none;
}
input[type="text"].ability
{
  width: 90%;
}
.secondary
{
  background: v-bind('secColor');
}
.primary
{
  background: v-bind('primColor');
  width:74%;
}
.alignment
{
  display: grid;
  grid-template-columns: auto auto auto;
  /* align-content: center; */
  width:280px;
  height:200px;
}
.LG
{
  background: #6dcff6;
  border: 5px solid black;
  width:85px;
  height:85px;
  opacity: 50%;
}
.NG
{
  background: #39b54a;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.CG
{
  background: #fff200;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.LN
{
  background: #0054a6;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.NN
{
  background: #b7b7b7;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;


}
.CN
{
  background: #f26522;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.LE
{
  background: #8560a8;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.NE
{
  background: #b33d42;
  border: 5px solid black;
    width:85px;
  height:85px;
  opacity: 50%;
}
.CE
{
  background: #ed1c24;
  border: 5px solid black;
    width:85px;
  height:85px;
    opacity: 50%;
}
.active
{
  opacity: 100%;
  border: 5px solid white;
}
</style>