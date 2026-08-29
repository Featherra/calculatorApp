<script setup>
import {ref} from 'vue'
import sound from '@/components/sound/quackAudio.m4a'

function soundPlay() {
  const audio = new Audio(sound)
  audio.play()
}

  let screen = ref('')

  function concatNum (num) {
    soundPlay()

    if (num === '.'){
      const parts = screen.value.split(/[+\-*/]/)
      const currentNum = parts.at(-1)

      if (currentNum.includes('.')){
        return
      }

    }

    screen.value += num
  }

  function concatOp(op) {
    const lastChar = screen.value.at(-1)

    if (screen.value === ''){
      if (op === '-'){
        screen.value = '-'
      }
    } else if (['+', '-', '*', '/', '.'].includes(lastChar)) {

    } else {
      screen.value += op
    }
  }

  function clearScreen() {
    screen.value = ''
  }

  function calculate (){

    const screenV = screen.value
    const lastChar = screenV.at(-1)

    if (['/', '+', '-', '*', '.'].includes(lastChar)) {
      return
    }

      const result = eval(screenV)
      screen.value = result.toString()


  }

</script>

<template>
  <main>
    <div id="calc">
      <div class="screen">{{screen}}</div>
      <div @click="clearScreen" class="btn clear">C</div>
      <div @click="calculate()" class="btn equal">=</div>

      <div @click="concatNum('1')" class="btn num">1</div>
      <div @click="concatNum('2')" class="btn num">2</div>
      <div @click="concatOp('*')" class="btn">*</div>

      <div @click="concatNum('3')" class="btn num">3</div>
      <div @click="concatNum('4')" class="btn num">4</div>
      <div @click="concatOp('+')" class="btn">+</div>

      <div @click="concatNum('5')" class="btn num">5</div>
      <div @click="concatNum('6')" class="btn num">6</div>
      <div @click="concatOp('-')" class="btn">-</div>

      <div @click="concatNum('7')" class="btn num">7</div>
      <div @click="concatNum('8')" class="btn num">8</div>
      <div @click="concatOp('/')" class="btn">/</div>

      <div @click="concatNum('9')" class="btn num">9</div>
      <div @click="concatNum('0')" class="btn num">0</div>
      <div @click="concatNum('.')" class="btn">.</div>

    </div>
  </main>
</template>

<style scoped>

main{
  display: flex;
  min-height: 80vh;
  align-items: center;
}
#calc{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 0 auto;
  width: 40%;
  border: 2px solid black;
  border-radius: 5px;
}

.screen{
  width: 100%;
  background-color: black;
  color: deepskyblue;
  text-align: right;
  font-size: 30px;
  padding: 15px;
  border: 1px solid blue;
}

.btn{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 26%;
  text-align: center;
  background-color: black;
  color: blue;
  margin: 5px;
  border-radius: 20px;
  padding: 8px 0 8px 0;
  cursor: pointer;
}

.btn:hover{
  transform: scale(110%);
}

.clear{
  border: 2px solid darkred;
  color: red;
  width: 35%;
}
.equal{
  border: 2px solid deepskyblue;
  color: deepskyblue;
  width: 35%;
}
</style>
