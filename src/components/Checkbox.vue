<template>
    <div class="checkbox_block">
        <input v-model="checked" type="checkbox">
        <img class="uncheck" @click='check' v-if="(checked==false)" src="../images/checkbox_normal.png" alt="">
        <img @click='check' v-else-if="checked==true" src="../images/checkbox_click.png" alt="">
        <span class="black_text">{{deduction.money}} <span class="gray_text">в {{deduction.year}}-ый год</span></span>
    </div>
</template>

<script>
    export default {
        name: 'Checkbox',
        props: {
          deduction: {
            type: Object
          }
        },
        data(){
            return{
                checked: this.deduction.checked
            }
        },
        methods: {
            check(){
                this.checked = !this.checked
            }
        },
        
}
</script>

<style scoped>
input{
    width: 20px;
    height: 20px;
    margin-left: 0;
    margin-right: 0;
    opacity: 0;
    position: relative;
  }
  img{
    width: 20px;
    height: 20px;
    margin-left: 0;
    position: relative;
    border-radius: 6px;
    left: -20px;
    box-sizing: border-box;
    cursor: url('../images/pointer.png'), pointer;
  }
  .uncheck:hover{
    border: 1px solid #000000;
  }
  .checkbox_block{
    position: relative;
    width: 100%;
    left: 0;
    border-bottom: 1px solid #DFE3E6;
    padding-bottom: 12px;
    margin-top: 16px;
  }
  .black_text{
    display: inline-block;
    position: relative;
    margin-top: 0;
    top: -5px;
    left: -10px;
    font-weight: normal;
    font-size: 14px;
    line-height: 24px;
    color: #000000;
  }
  .gray_text{
    display: inline-block;
    position: relative;
    margin-top: 0;
    color: #808080;
  }
</style>