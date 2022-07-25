<template>
  <main>
    <section class="coming-soon">
      <div>
        <h2>
          Looking forward to New Year 2023!
          <br><br><br><br>
          <span>(Ukrainian time)</span>
        </h2>

        <div class="countdown">
          <timer-block label="Days" :count="remainingDays"></timer-block>
          <timer-block label="Hours" :count="remainingHours"></timer-block>
          <timer-block label="Minutes" :count="remainingMinutes"></timer-block>
          <timer-block label="Seconds" :count="remainingSeconds"></timer-block>
        </div>


      </div>
      <img class="waiting" src="https://therapyzen.com/Content/img/Calendar-hero.png" alt="">
    </section>
  </main>
</template>

<script lang="ts" setup>
import { ref,onMounted,onUnmounted } from'vue'

import TimerBlock from '@/components/TimerBlock.vue'
// import ref from 'vue'
  const newYears = "1 Jan 2024"

  const remainingDays = ref("")
  const remainingHours = ref("")
  const remainingMinutes = ref("")
  const remainingSeconds = ref("")
  function countdown(){
    const newYearDate : Date = new Date(newYears)
    const currentDate : Date = new Date()
    
    const totalSeconds = (newYearDate.getTime() - currentDate.getTime()) / 1000;

    const days = Math.floor(totalSeconds / 3600 / 24);
    const hours = Math.floor(totalSeconds / 3600) % 24;
    const mins = Math.floor(totalSeconds / 60) % 60;
    const seconds = Math.floor(totalSeconds) % 60;

    remainingDays.value = setTime(days)
    remainingHours.value = setTime(hours)
    remainingMinutes.value = setTime(mins)
    remainingSeconds.value = setTime(seconds)

  }

  function setTime(value : number){
    return value > 10 ? value.toString() : `0${value}`
  }

  let timeInterval : ReturnType<typeof setInterval>
  onMounted(
    ()=>{
      timeInterval = setInterval(countdown,1000)
    }
  )

  onUnmounted(
    ()=>{
      clearInterval(timeInterval)
    }
  )
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Lato", sans-serif;
  color: #404244;
}

ul {
  padding: 0;
  margin: 0;
  list-style: none;
}

h2 {
  font-size: 3.5rem;
  font-weight: bold;
  padding: 3rem;
  text-align: center;
}

h2 span {
  background: linear-gradient(to bottom, #005bbb 50%, #ffd500 80%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.coming-soon {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.countdown {
  display: flex;
  justify-content: space-around;
  text-align: center;
}

.waiting {
  height: 50vh;
}
</style>
