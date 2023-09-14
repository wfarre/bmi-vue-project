<script setup lang="ts">
import { ref } from 'vue'
import FormComponent from './FormComponent.vue'

const bmi = ref(0)
const minIdealWeight = ref(0)
const maxIdealWeight = ref(0)
const imperialIsChecked = ref(false)
</script>

<template>
  <header class="header">
    <div class="logo">
      <img src="../../assets/images/logo.svg" alt="" />
    </div>

    <div class="header__header">
      <h1 class="title">
        Body Mass<br />
        Index Calculator
      </h1>

      <p class="text">
        Better understand your weight in relation to your height using our body mass index (BM)
        calculator. While BMI is not the sole determinant of a healthy weight, it offers a valuable
        starting point to evaluate your overall health and well-being.
      </p>
    </div>

    <div class="header__footer">
      <FormComponent
        @response="
          (res: any) => {
            bmi = parseFloat(res.result.value)
            minIdealWeight = res.minIdealWeight.value
            maxIdealWeight = res.maxIdealWeight.value
            imperialIsChecked = res.imperialIsChecked.value
          }
        "
      />

      <div v-if="bmi !== 0" class="result">
        <div class="bmi">
          <h3 class="title">Your bmi is...</h3>
          <p class="bmi__result">{{ bmi.toFixed(1) }}</p>
        </div>

        <p class="advice">
          Your BMI suggests you’re a healthy weight. Your ideal weight is between
          {{
            imperialIsChecked
              ? (minIdealWeight / 14).toFixed().toString() +
                'st' +
                (minIdealWeight % 14).toFixed().toString() +
                'lbs - ' +
                (maxIdealWeight / 14).toFixed().toString() +
                'st' +
                (maxIdealWeight % 14).toFixed().toString() +
                'lbs.'
              : minIdealWeight.toFixed().toString() +
                'kg - ' +
                maxIdealWeight.toFixed().toString() +
                'kg.'
          }}
        </p>
      </div>

      <div v-if="bmi === 0" class="welcome">
        <h3 class="title">Welcome</h3>
        <p class="content">Enter your height and weight and you’ll see your BMI result here</p>
      </div>
    </div>
  </header>
</template>

<style lang=""></style>
