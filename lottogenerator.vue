<template>
<div>
    <div>당첨 숫자</div>
    <div id = '결과창'>
        <lotto-ball v-for = 'ball in winBalls' :key = 'ball' :number = 'ball'></lotto-ball>
    </div>
    <div>보너스</div>
    <lotto-ball v-if = 'bonus' :number = 'bonus'></lotto-ball>
    <input type="button" value = '한번 더!' v-if = 'redo'>
</div>
</template>

<script>

import LottoBall from './LottoBall';

function getWinNumber() {
    console.log('getWinNumber');
    const candidate = Array(45).fill().map((v, i) => i + 1);
    const shuffle = [];
    while (candidate.length > 0) {
        shuffle.push(candidate.splice(Math.floor(Math.random() *candidate.length), 1)[0]);
    }
    const bonusNumber = shuffle[shuffle.length - 1];
    const winNumbers = shuffle.slice(0, 6).sort((p, c) => p - c);
    return [...winNumbers, bonusNumber];
}

 export default {
     components: {
         'lotto-ball' : LottoBall,
     },
     data () {
         return {
             winNumbers: getWinNumber(),
             redo: false,
             bonus : null,
             winBalls: [],            
         }
     },
     computed: {
         
     },
     methods: {
         
     },
     mounted() {
         for (let i = 0; i < this.winNumbers.length - 1; i++) {
             setTimeout(() => {
                 this.winBalls.push(this.winNumbers[i]);
             }, (i + 1) * 1000)
             console.log(this.winNumbers)
         }
         setTimeout(() => {
             this.bonus = this.winNumbers[6];
             this.redo = true;
         }, 7000);
     },
     beforeDestroy() {
         console.log('beforeDestroy');
     },
     watch: {
     },
 }
</script>

<style scoped>
#computer {
    width: 142px;
    height: 200px;
    background-position: 0 0;
}
</style>