<template>
  <div class="image-show" @mouseout="runInv" @mouseover="clearInv"> 
    <div class="image-img">
    	<a>
      	<transition name="image-trans">
        	<img v-if="isShow" :src="images[nowIndex].img">
      	</transition> 
      	<transition name="image-trans-old">
       	 <img v-if="!isShow" :src="images[nowIndex].img">
      	</transition>
      </a>
    </div>
    <div class="prepage" @click="goto(prevIndex)">&lt</div>
    <div class="nextpage" @click="goto(nextIndex)">&gt</div>
    <ul class="image-pages">
      <li v-for="(item, index) in images" @click="goto(index)">
        <a :class="{on:index === nowIndex}">{{index + 1}}</a>
      </li>
    </ul> 
  </div>
</template>

<script>
export default {
  props: {
    images:{
      type: Array,
      default: []
    }
  },
  data () {
    return {
      nowIndex: 0,
      isShow: true
    }
  },
  computed: {
    prevIndex () {
      if (this.nowIndex === 0) {
        return this.images.length - 1
      }
      else {
        return this.nowIndex - 1
      }
    },
    nextIndex () {
      if (this.nowIndex === this.images.length-1) {
        return 0
      }
      else {
        return this.nowIndex + 1
      }
    }
  },
  methods: {
    goto (index) {
      this.isShow = false
      setTimeout(() => {
        this.isShow = true
        this.nowIndex = index
      }, 10)
    },
    runInv () {
      this.invId = setInterval(()=>{
        this.goto(this.nextIndex)
      },3000)
    },
    clearInv () {
      clearInterval(this.invId)
    }
  },
  mounted () {
    this.runInv();
  }
}
</script>

<style scoped>
.image-trans-enter-active {
  transition: all .5s;
}
.image-trans-enter {
  transform: translateX(700px);
}
.image-trans-old-leave-active {
  transition: all .5s;
  transform: translateX(-700px);
}
.image-show {
  border: 3px solid #888;
  position: relative;
  margin: 20px auto;
  width: 700px;
  height: 480px;
  overflow: hidden; 
}
.image-img {
  width:100%;
}
.image-img img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
}
.prepage {
  position: absolute;
  padding: 0 10px;
  cursor: pointer;
  color: #eee;
  font-size: 80px;
  top: 40%;
}
.nextpage {
  position: absolute;
  padding: 0 10px;
  cursor: pointer;
  color: #eee;
  font-size: 80px;
  top: 40%;
  right: 0;
}
.image-pages {
  position: absolute;
  bottom: 0;
  margin: 5px;
  padding: 0;
  right: 0;
  left: 0;
  text-align: center;
}
.image-pages li {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
  color: #05f;
  font-size: 16px;
}
.image-pages li .on {
  color: deeppink;
}
</style>