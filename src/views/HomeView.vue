<template>
  <div class="home">
    <NavBar/>
    <div class="container" >
      <div class="header">
        <h1>Welcome</h1>
        <button class="btn-generate" @click="generateLine">Generate a Pickup Lline</button>
      </div>
      <transition name="switch" mode="out-in" appear>
        <div class="lines" v-if="this.linesArr.length">
            <transition-group name="lContainer" tag="div" appear class="lines-container">
              <div class="line-container" v-for="line in linesArr" :key="line">
                <p id="demo">{{line}}</p>
                <div class="icons">
                  <Icon class="icon" icon="akar-icons:sound-on" @click="speakUp(line)"/>
                  <div class="line-ver"></div>
                  <Icon class="icon" icon="mingcute:delete-2-line" @click="deleteLine(line)"/>
                </div>
              </div>
            </transition-group>
        </div>
        <div v-else class="intro">
            <p>Welcome to Pickup Line Generator. Ready to take your flirting game to the next level? Let our pickup line generator be your guide.</p>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import NavBar from "../components/NavBar.vue"
import { Icon } from '@iconify/vue';
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {NavBar, Icon},
  data(){
    return{
      linesArr:[],
      line:"",
      i :0,
      speed :50
    }
  },
  methods:{
    generateLine(){
      let random = Math.round(Math.random()*57)
      fetch("http://localhost:3000/pickupLines",{
      method: 'GET',
    }).then((response)=>response.json())
    .then((data)=>{
        this.line = data[random].body
        console.log(this.line);
        this.linesArr.push(this.line)
      })
    },
    speakUp(line){
      var msg = new SpeechSynthesisUtterance(line);
      window.speechSynthesis.speak(msg);
    },
    deleteLine(line){
      console.log(this.linesArr.indexOf(line))
      this.linesArr.splice(this.linesArr.indexOf(line),1)
    }
  }
}
</script>
<style scoped>
.container{
  padding: 2rem 16rem;
}
.header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.btn-generate{
  background-color: #fc2069;
  border: none;
  padding: 10px 24px;
  color: #fff;
  border-radius: 24px;
  font-weight: 900;
  cursor: pointer;
  transition: all 0.1s;
}
.btn-generate:active{
  transform: scale(0.95);
}
.btn-generate:hover{
  background-color: #ff1462;
}
.lines-container{
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  align-items: flex-start;
  row-gap: 24px;
}
.line-container{
  /* margin: 0 auto; */
  width: 48%;
  border-radius: 12px;
  background-color: #fff;
  overflow: hidden;
  /* animation: fadePop 0.4s ease-in-out; */
}
/* @keyframes fadePop {
  from{
    transform: scale(0);
    opacity: 0;
  }
  to{
    transform: scale(1);
    opacity: 1;
  }
} */
.line-container p{
  padding: 12px;
}
.icons{
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  background-color: #3d2fff;
}
.icons .icon{
  width: 32px;
  height: 32px;
  padding: 16px 48px;
  color: #fff;
  cursor: pointer;
}
.line-ver{
  width: 1px;
  height: 64px;
  background-color: #fff;
}
.line-container p{
  margin-top: 0;
  font-size: 24px;
  line-height: 30px;
}
.intro{
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  font-size: 20px;
  max-width: 600px;
  margin: 72px auto 0;
}
.lContainer-enter-from,
.lContainer-leave-to{
  opacity: 0;
  transform: translateY(60px);
}
.lContainer-enter-to,
.lContainer-leave-from{
  opacity: 1;
  transform: translateY(0);
}
.lContainer-enter-active,
.lContainer-leave-active{
  transition: all 0.5s ease-in-out;
}

.switch-enter-from,
.switch-leave-to{
  opacity: 0;
  transform: translateX(60px);
}
.switch-enter-to,
.switch-leave-from{
  opacity: 1;
  transform: translateX(0);
}
.switch-enter-active,
.switch-leave-active{
  transition: all 0.5s ease-in-out;
}
</style>
