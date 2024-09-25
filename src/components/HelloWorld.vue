<script setup>
import { ref } from 'vue'
import { data } from './list/dt.js'

const score = ref(0)
const deprScore = ref(100)
const isScoreVisible = ref(false)
const isFake = ref(false);
const mapIs = data.map(() => false);

const toggleHandler = (event, value, index) => {
  if (event.target.checked) {
    score.value += value
    deprScore.value--;
    mapIs[index] = true;
  } else {
    score.value -= value
    deprScore.value++;
    mapIs[index] = false;
  }
}

// Функция для расчета и отображения результата
const calculateScore = () => {
  isScoreVisible.value = true;
  isFake.value = deprScore.value > 95;
  // const progressBar = document.querySelector('.progressBar');
  // console.log(progressBar);
  // progressBar.value = score.value;
}

const getEmo = (val) => {
  if (val < 100) {
    return '&#128519;'; // 😏
  } else if (val < 300) {
    return '&#128513;'; // 😃
  } else if (val < 450) {
    return '&#128522;'; // 😊
  } else if (val < 550) {
    return '&#129321;'; // 😱
  } else if (val < 630) {
    return '&#129312;'; // 😲
  } else if (val < 750) {
    return '&#128520;'; // 😄
  } else if (val < 980) {
    return '&#129397;'; // 😏
  } else if (val < 1200) {
    return '&#129319;'; // 😓
  } else if (val < 1350) {
    return '&#129322;'; // 😆
  } else if (val < 1480) {
    return '&#129313;'; // 😃
  } else if (val >= 1480) {
    return '&#128169;'; // 💩
  }
}

</script>

<template>
  <div class="container">
    <h1>{{ msg }}</h1>

    <div v-if="!isScoreVisible" >
      <div class="questions">
        <div v-for="(item, index) in data" :key="index" class="question-item">
          <label>
            <input type="checkbox" @change="(event) => toggleHandler(event, item.value, index)" />
            <span>{{ index + 1 }}. {{ item.ans }}</span>
          </label>
        </div>
      </div>
      <button class="calculate-btn" @click="calculateScore">Calculate My Score!</button>
    </div>

    <div v-else class="result">
      <h2 class="resultName">Your score: </h2>
      <div v-if="!isFake">
        <h1 class="resultVal">{{ score }}<span class="dv"> / </span>{{ deprScore }} </h1>
        <div class="wrapProgress" >
          <span style="font-size: 1.2em;">&#128037;</span>
          <progress class="progressBar" :value="score" max="1741" ></progress>
          <span style="font-size: 1.2em;">&#128128;</span>
        </div>
        <span v-html="getEmo(score)" style="font-size: 2.5em;"></span>
      </div>
      <h1 v-else class="resultVal"> <span> try later </span> </h1>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 0px;
}

h1 {
  font-size: 2rem;
  text-align: center;
}

.questions {
  height: calc(100vh - 310px);
  overflow: auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.question-item {
  display: flex;
  align-items: flex-start;
  border: 2px dashed #f677ff;
  border-radius: 5px;
  color: #1a1a1a;
}

label{
  display: flex;
  width: 100%;
  cursor: pointer;
  /*cursor: url('../assets/icons8-64.png') 2 2, auto;*/
  padding: 10px;
}

input[type="checkbox"] {
  display: block;
  margin-right: 10px;
  transform: scale(1.3);
}

span {
  font-size: 1rem;
  text-align: left;  /* Выравнивание по левому краю */
}

.calculate-btn {
  color: #8d7994;
  width: 60%;
  padding: 15px;
  background-color: #d8d56d;
  font-size: 1.2rem;
  border: none;
  border-radius: 15px;
  margin: 15px auto;
}

.calculate-btn:hover {
  background-color: #45a049;
}

.result {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-weight: bold;
}

.wrapProgress {
  margin: 20px 0;
  display: flex;
  flex-direction: row;
  gap: 8px;
  align-items: center;
}

.progressBar {
  width: 250px;
  height: 25px;
}

.dv {
  color: #1a1a1a;
  font-size: inherit;
}

.resultName {
  color: #1a1a1a;
  font-size: 150%;
  margin-top: 120px ;
}

.resultVal {
  color: #f40a06;
  font-size: 300%;
  font-weight: bold;
  margin: 0;
  padding: 0;
}

@media (max-width: 600px) {
  h1 {
    font-size: 1.5rem;
  }

  .questions {
    height: calc(100vh - 210px);
    gap: 10px;
  }

  .question-item {
    flex-direction: column;
    gap: 10px;
    border: 0;
  }

  label{
    width: auto;
    min-width: 100px;
    padding: 5px 8px;
    cursor: auto;
  }

  span {
    font-size: 0.9rem;
  }

  .calculate-btn {
    font-size: 1rem;
  }

  .result {
    font-size: 1.5rem;
  }
}
</style>
