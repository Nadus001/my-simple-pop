<script setup>
import { ref } from 'vue'
import { data } from './list/dt.js'

const score = ref(0)
const deprScore = ref(100)
const isScoreVisible = ref(false)
const isFake = ref(false);

const toggleHandler = (event, value) => {
  if (event.target.checked) {
    score.value += value
    deprScore.value--;
  } else {
    score.value -= value
    deprScore.value++;
  }
}

// Функция для расчета и отображения результата
const calculateScore = () => {
  isScoreVisible.value = true;
  isFake.value = deprScore.value > 95;
}
</script>

<template>
  <div class="container">
    <h1>{{ msg }}</h1>

    <div v-if="!isScoreVisible" >
      <div class="questions">
        <div v-for="(item, index) in data" :key="index" class="question-item">
          <label>
            <input type="checkbox" @change="(event) => toggleHandler(event, item.value)" />
            <span>{{ index + 1 }}. {{ item.ans }}</span>
          </label>
        </div>
      </div>
      <button class="calculate-btn" @click="calculateScore">Calculate My Score!</button>
    </div>

    <div v-else class="result">
      <h2 class="resultName">Your score: </h2>
      <h1 v-if="!isFake" class="resultVal">{{ score }}<span class="dv"> / </span>{{ deprScore }} </h1>
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
  cursor: pointer;
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
