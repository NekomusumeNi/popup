<template>
    <div class="popup-container">
      <div class="popup-content">
        <div>
        <img @click="$emit('close-popup')" class="close" src="../images/close.png" alt="">
        <h2>Налоговый вычет</h2>
        <p>Используйте налоговый вычет чтобы погасить ипотеку досрочно. Размер налогового вычета составляет не более 13% от своего официального годового дохода.</p>
        <span class="blackspan">Ваша зарплата в месяц</span>
        <input :class='{"wage-error": error==true }' @click="errorCheck" v-model="wage" id="wage" type="text" placeholder="Введите данные">
        <label :class='{"label-error": error==true }' v-if="error == true" for="wage">Поле обязательно для заполнения</label>
        <span @click="calculation" class="redspan">Рассчитать</span>
        <Calc
            :deductions = 'deductions'
        />
        <span class="blackspan">Что уменьшаем?</span> 
        <button 
            @click='payment' 
            :class="{'tag-button-active':termStatus == false, 'tag-button-disable':termStatus == true}"
        >
            <span>Платёж</span>
        </button> 
        <button 
            @click='term'
            :class="{'tag-button-active':termStatus == true, 'tag-button-disable':termStatus == false}"
        >
            <span>Срок</span>
        </button>
        </div>
        <button class="big-button"><span>Добавить</span></button>
      </div>
    </div>
</template>

<script>
    import Calc from '@/components/Calc.vue'

    export default {
        name: 'Popup',
        props: {
            popup_visibility: {
                type: String
            }
        },
        data(){
            return{
                deductions: [
                    
                ],
                error: false,
                wage: '',
                termStatus: false
            }
        },
        methods: {
            calculation(){
                this.wage = Number(this.wage)
                if(this.wage === this.wage && this.wage != 0){
                    this.deductions = []
                    let balance = 260000
                    let sum = this.wage*12*0.13
                    for(let idx = 1; balance>0; idx++){
                        if(balance > sum){
                            this.deductions.push(
                                {id: Date.now()*Math.random(), money: sum, year: idx, checked: this.termStatus}
                            )
                            balance = balance - sum
                        } else{
                            this.deductions.push(
                                {id: Date.now()*Math.random(), money: balance, year: idx, checked: this.termStatus}
                            )
                            balance = balance - sum
                        }
                    }
                }
                else{ this.error = !this.error
                this.wage = ''}
            },
            errorCheck(){
                if(this.error){
                    this.error = !this.error
                }
            },
            payment(){
                this.termStatus = false
            },
            term(){
                this.termStatus = true
                if(this.deductions.length > 0){
                    this.deductions = []
                    let balance = 260000
                    let sum = this.wage*12*0.13
                    for(let idx = 1; balance>0; idx++){
                        if(balance > sum){
                            this.deductions.push(
                                {id: Date.now()*Math.random(), money: sum, year: idx, checked: this.termStatus}
                            )
                            balance = balance - sum
                        } else{
                            this.deductions.push(
                                {id: Date.now()*Math.random(), money: balance, year: idx, checked: this.termStatus}
                            )
                            balance = balance - sum
                        }
                    }
                }
            }
        },
        components: {
            Calc
        }
}
</script>

<style scoped>
  .popup-container{
    position: absolute;
    width: 100%;
    height: 100%;
    background: #B3B3B3;
    
  }
  .popup-content{
    position: absolute;
    width:  552px;
    padding: 32px;
    box-sizing: border-box;
    background: #FFFFFF;
    border-radius: 30px;
    top: 10%;
    left: 50%;
    transform: translateX(-50%);
  }
  .close{
    position: absolute;
    top: 27px;
    right: 27px;
    cursor: url('../images/pointer.png'), pointer;
  }

  .popup-content h2{
    font-weight: 500;
    font-size: 28px;
    line-height: 40px;
    margin-top: 0;
    margin-bottom: 16px;
  }

  .popup-content p{
    color: #808080;
    font-weight: normal;
    font-size: 14px;
    line-height: 24px;  
    padding-right: 30px;
    margin: 0;
  }

  .blackspan{
    display: inline-block;
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    margin-right: 32px;
    margin-top: 24px;
  }

  .redspan{
    display: block;
    margin-top: 8px;
    margin-bottom: 4px;
    color: #EA0029;
    font-weight: 500;
    font-size: 14px;
    line-height: 24px;
    transition: 0.2s;
  }

  .redspan:hover{
    color: #F53A31;
    cursor: url('../images/pointer.png'), pointer;
  }
  
  .big-button{
    width: 100%;
    background: linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56;
    border: 0;
    border-radius: 6px;
    height: 56px;
    margin-top: 40px;
    position: relative;
    flex-shrink: 0;
  }

  .big-button span{
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    color: #FFFFFF;
  }
  .tag-button-active{
    background: linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56;
    border-radius: 50px;
    height: 36px;
    padding: 6px 12px;
    box-sizing: border-box;
    border: 0;
    margin-right: 16px;
  }

  .tag-button-active span{
    color: #FFFFFF;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 24px;
  }

  .tag-button-disable{
    background: #EEF0F2;
    border-radius: 50px;
    height: 36px;
    padding: 6px 12px;
    box-sizing: border-box;
    color: #000;
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 24px;
    border: 0;
    margin-right: 16px;
    transition: 0.4s;
  }
  .tag-button-disable:hover{
    background: #DFE3E6
  }
  #wage{
    width: 100%;
    border: 1px solid #DFE3E6;
    box-sizing: border-box;
    padding: 8px 10px;
    height: 40px;
    border-radius: 3px;
    margin-top: 6px;
  }
  #wage:hover{
    border: 1px solid #000000;
  }
  #wage:focus{
    outline: none;
  }
  
  .wage-error{
    border: 1px solid #EA0029 !important;
  }
  .label-error{
    font-size: 10px;
    line-height: 12px;
    color: #EA0029;
  }


  @media all and (max-width: 414px){
      .popup-content{
        position: relative;
        width: 100%;
        min-height: 100%;
        padding: 32px 16px 16px 16px;
        box-sizing: border-box;
        background: #FFFFFF;
        border-radius: 0;
        top: 0;
        left: 0;
        transform: none;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
      }

      .big-button{
        max-width: 100%;
        background: linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56;
        border: 0;
        border-radius: 6px;
        height: 56px;
       
        position: relative;
        flex-shrink: 0;
        box-sizing: border-box;
    }
    .blackspan{
        width: 80%;
    }
    .tag-button-active{
        margin-top: 24px;
    }
    .tag-button-disable{
        margin-top: 24px;
    }
    .popup-content p{
        font-size: 12px;
        padding-right: 10px;
    }
  }

  @media all and (max-width: 768px){
      .popup-content{
            width:  453px;
        }

        .popup-content p{
            padding-right: 36px;
        }
  }
</style>