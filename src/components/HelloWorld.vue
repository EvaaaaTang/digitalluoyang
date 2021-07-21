<template>
<div >
  <!-- Hero -->
  <img class="bg" :src="bgsrc">
  <section class="et-hero-tabs">
    <div class="et-hero-tabs-container">
      <a class="et-hero-tab" href="#tab-es6">{{$t('m.landingtitle')}}</a>
      <a class="et-hero-tab" href="#tab-flexbox">{{$t('m.experience')}}</a>
      <a class="et-hero-tab" href="#tab-react">{{$t('m.research')}}</a>
      <a class="et-hero-tab" href="#tab-angular">{{$t('m.joinus')}}</a>
      <a class="et-hero-tab" href="#tab-other">{{$t('m.about')}}</a>
      <span class="et-hero-tab-slider"></span>
    </div>
  </section>
   <!-- Main -->
  <main class="et-main">
    <section class="et-slide" id="tab-es6">
      <h1>{{$t('m.landingtitle')}}</h1>
      <a href="javascript:void(0);" @click="toChinese()">中文</a>
      <a href="javascript:void(0);" @click="toEnglish()">ENGLISH</a>
    </section>
    <section class="et-slide" id="tab-flexbox">
      <h1>{{$t('m.experience')}}</h1>
  
    </section>
    <section class="et-slide" id="tab-react">
      <h1>{{$t('m.research')}}</h1>
   
    </section>
    <section class="et-slide" id="tab-angular">
      <h1>{{$t('m.joinus')}}</h1>
     
    </section>
    <section class="et-slide" id="tab-other">
      <h1>{{$t('m.about')}}</h1>
    
    </section>
  </main>
</div>
</template>




<script >
import $ from 'jquery'
import 'jquery.ripples'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      currentId:"",
      curretnTab:"",
      tabContainerHeight:70,
      bgsrc:require('@/assets/temple.jpeg')
    }
  },
  created(){
    this.currentId = null;
    this.currentTab = null;
    this.tabContainerHeight = 70;

  },
  mounted(){
    let self=this;
    $('.et-hero-tab').click(function() { 
      self.onTabClick(event, $(this)); 
    });
    $(window).scroll(() => { this.onScroll(); });
    $(window).resize(() => { this.onResize(); });
    $('.et-main').ripples(
          {	resolution: 512,
      dropRadius: 20,
      perturbance: 0.01}
      );
  },
  methods:{
  onTabClick(event, element) {
    event.preventDefault();
    let scroll = $(element.attr('href')).offset().top - this.tabContainerHeight + 1;
    $('html, body').animate({ scrollTop: scroll }, 600);
  },
  onScroll() {
    this.checkTabContainerPosition();
    this.findCurrentTabSelector();
  },
  
  onResize() {
    if(this.currentId) {
      this.setSliderCss();
    }
  },
  
  checkTabContainerPosition() {
    let offset = $('.et-hero-tabs').offset().top + $('.et-hero-tabs').height() - this.tabContainerHeight;
    if($(window).scrollTop() > offset) {
      $('.et-hero-tabs-container').addClass('et-hero-tabs-container--top');
    } 
    else {
      $('.et-hero-tabs-container').removeClass('et-hero-tabs-container--top');
    }
  },
  
  findCurrentTabSelector(element) {
    let newCurrentId;
    let newCurrentTab;
    let self = this;
    $('.et-hero-tab').each(function() {
      let id = $(this).attr('href');
      let offsetTop = $(id).offset().top - self.tabContainerHeight;
      let offsetBottom = $(id).offset().top + $(id).height() - self.tabContainerHeight;
      if($(window).scrollTop() > offsetTop && $(window).scrollTop() < offsetBottom) {
        newCurrentId = id;
        newCurrentTab = $(this);
      }
    });
    if(this.currentId != newCurrentId || this.currentId === null) {
      this.currentId = newCurrentId;
      this.currentTab = newCurrentTab;
      this.setSliderCss();
    }
  },
  
  setSliderCss() {
    let width = 0;
    let left = 0;
    if(this.currentTab) {
      width = this.currentTab.css('width');
      left = this.currentTab.offset().left;
    }
    $('.et-hero-tab-slider').css('width', width);
    $('.et-hero-tab-slider').css('left', left);
  },
  toChinese(){
    this.$i18n.locale = 'zh-CN'	
  },
  toEnglish(){
    this.$i18n.locale = 'en-US'	
  }
  

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

Result Skip Results Iframe body {
	 font-family: "Century Gothic", 'Lato', sans-serif;
}
 a {
	 text-decoration: none;
}
.et-slide {
	 display: flex;
	 flex-direction: column;
	 justify-content: center;
	 align-items: center;
	 height: 100vh;
	 position: relative;
	 background:transparent;
	 text-align: center;
	 padding: 0 2em;
}
.et-hero-tabs{
  display: flex;
	 flex-direction: column;
	 justify-content: center;
	 align-items: center;
	 height: 70px;
	 position: relative;
	 background: #eee;
	 text-align: center;
	 padding: 0 2em;
}
 .et-hero-tabs h1, .et-slide h1 {
	 font-size: 2rem;
	 margin: 0;
	 letter-spacing: 1rem;
}
 .et-hero-tabs h3, .et-slide h3 {
	 font-size: 1rem;
	 letter-spacing: 0.3rem;
	 opacity: 0.6;
   /* display:inline; */
}
.et-slide a:focus{
  font-size: 3rem;
  opacity:0.6;
  color:black;
}
.et-slide a{
  font-size: 3rem;
  color:black;
}
 .et-hero-tabs-container {
	 display: flex;
	 flex-direction: row;
	 position: absolute;
	 bottom: 0;
	 width: 100%;
	 height: 70px;
	 box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
	 background: #fff;
	 z-index: 10;
}
 .et-hero-tabs-container--top {
	 position: fixed;
	 top: 0;
}
.et-main{
  background: url('../assets/temple.jpeg') no-repeat;
  background-size:100% 100% 
}
 .et-hero-tab {
	 display: flex;
	 justify-content: center;
	 align-items: center;
	 flex: 1;
	 color: #000;
	 letter-spacing: 0.1rem;
	 transition: all 0.5s ease;
	 font-size: 0.8rem;
}
 .et-hero-tab:hover {
	 color: white;
	 background: rgba(102, 177, 241, 0.8);
	 transition: all 0.5s ease;
}
 .et-hero-tab-slider {
	 position: absolute;
	 bottom: 0;
	 width: 0;
	 height: 6px;
	 background: #66b1f1;
	 transition: left 0.3s ease;
}
 @media (min-width: 800px) {
	 .et-hero-tabs h1, .et-slide h1 {
		 font-size: 10rem;
     color:black;
	}
	 .et-hero-tabs h3, .et-slide h3 {
		 font-size: 5rem;
     color:black;
	}
	 .et-hero-tab {
		 font-size: 1rem;
	}
}
.bg{
  position:absolute;
  z-index:-1;
  text-align: center;
  left:20%;
  right:20%;
  width:60%;
  /* height:100%; */
}
</style>
