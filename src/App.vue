<template>
  <div>
    <button @click='PopUpOpen' class="main-button"><span> Налоговый вычет</span></button>
    <Popup 
      v-if="popup_visibility == 'visible'"
      :popup_visibility='popup_visibility'
      @close-popup="closePopup"
    />
  </div>
</template>

<script>
import Popup from '@/components/Popup.vue'

export default {
  name: 'App',
  data(){
    return {
      popup_visibility: 'hide',
    }
  },
  methods: {
    PopUpOpen(){
      this.popup_visibility = 'visible'
      document.body.style.background = '#B3B3B3'
    },
    closePopup(){
        this.popup_visibility = 'hide'
        document.body.style.background = 'linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56'
    }
  },
  components: {
    Popup
  }
}
</script>

<style>
@import url('./fonts/fonts.css');
  button:hover{
    cursor: url('./images/pointer.png'), pointer;
  }
  body{
    margin:0;
    background: linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56;
    box-shadow: 0px -0.11px 16.9495px rgba(183, 187, 225, 0.33);
    font-family: 'Lab Grotesque';
    height: 100%;
  }
  .main-button{
    border: 1px solid #FFFFFF;
    width: 198px;
    height: 56px;
    border-radius: 6px;
    box-sizing: border-box;
    background-color: inherit;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    filter: drop-shadow(0px 0px 44px #CFDAE7);
    transition: 0.4s;
  }
  .main-button:hover{
    background-color: #fff;
    filter: none;
  }
  .main-button:hover span{
    color: #000;
  }
  .main-button span{
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    color: #FFFFFF;
  }

  @media all and (max-width: 414px){
      .big-button{
        position: relative;
        bottom: 0;
      }
  }
</style>
