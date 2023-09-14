<script setup lang="ts">
import { ref, watch } from 'vue'

const emit = defineEmits(['response'])
// const emitMaxIdeal = defineEmits(['weight']);

// const emit = defineEmits(['response'])

// emit with argument
// emit('response', 'hello from child')
const minIdealWeight = ref(0)
const maxIdealWeight = ref(0)

const imperialClass = ref('')
const imperialIsChecked = ref(false)
const dynamicIdHeight = ref('meters')
const dynamicIdWeight = ref('kg')

const meterValue = ref('')
const kiloValue = ref('')
const inchValue = ref('')
const lbsValue = ref('')

const height = ref(0)
const weight = ref(0)
const result = ref(0)

const handleChange = (e: any) => {
  const dataType = e.target.attributes['data-type'].value
  const input = isNaN(parseFloat(e.target.value)) ? 0 : parseFloat(e.target.value)

  if (!imperialIsChecked.value) {
    if (dataType === 'meters') {
      height.value = input
    }

    if (dataType === 'kg') {
      weight.value = input
    }
  }

  if (imperialIsChecked.value) {
    const feet = isNaN(parseFloat(meterValue.value)) ? 0 : parseFloat(meterValue.value)
    const inch = isNaN(parseFloat(inchValue.value)) ? 0 : parseFloat(inchValue.value)
    const stone = isNaN(parseFloat(kiloValue.value)) ? 0 : parseFloat(kiloValue.value)
    const lbs = isNaN(parseFloat(lbsValue.value)) ? 0 : parseFloat(lbsValue.value)

    if (dataType === 'feet' || dataType === 'inch') {
      height.value = feet * 12 + inch
    }

    if (dataType === 'st' || dataType === 'lbs') {
      weight.value = stone * 14 + lbs
    }
  }

  if (imperialIsChecked.value) {
    result.value = calculateImperialBmi(height.value, weight.value)
    minIdealWeight.value = calculateImperialWeight(18.5, height.value)
    maxIdealWeight.value = calculateImperialWeight(24.5, height.value)
  } else {
    result.value = calculateMetricBmi(height.value, weight.value)
    minIdealWeight.value = calculateMetricWeight(18.5, height.value)
    maxIdealWeight.value = calculateMetricWeight(24.5, height.value)
  }
}

const handleChecked = (e: any) => {
  const checkedValue = e.target.value

  meterValue.value = ''
  kiloValue.value = ''
  inchValue.value = ''
  lbsValue.value = ''
  result.value = 0
  height.value = 0
  weight.value = 0
  minIdealWeight.value = 0
  maxIdealWeight.value = 0

  if (checkedValue === 'metric') {
    imperialIsChecked.value = false
    imperialClass.value = ''
    dynamicIdHeight.value = 'meters'
    dynamicIdWeight.value = 'kg'
  }
  if (checkedValue === 'imperial') {
    imperialIsChecked.value = true
    imperialClass.value = 'imperial'
    dynamicIdHeight.value = 'feet'
    dynamicIdWeight.value = 'st'
  }
}

const calculateMetricBmi = (height: number, weight: number) => {
  if (height !== 0) {
    return weight / (height * height)
  } else {
    return 0
  }
}

const calculateImperialBmi = (height: number, weight: number) => {
  if (height !== 0) {
    return (weight / (height * height)) * 703
  } else {
    return 0
  }
}

const calculateImperialWeight = (bmi: number, height: number) => {
  return (bmi * height * height) / 703
}

const calculateMetricWeight = (bmi: number, height: number) => {
  return bmi * height * height
}

watch(result, () => {
  emit('response', { result, minIdealWeight, maxIdealWeight, imperialIsChecked })
  console.log(result.value)
  console.log(weight.value)

  console.log(height.value)
})
</script>

<template lang="">
  <div>
    <form class="form" action="">
      <h2 class="instructions">Enter your details below</h2>

      <div class="units">
        <label class="label" for="metric"
          >metric
          <input
            class="radio"
            type="radio"
            name="unit"
            id="metric"
            value="metric"
            checked
            @change="handleChecked"
          />
          <span class="checkmark"></span>
        </label>

        <label for="imperial" class="label"
          >imperial
          <input
            class="radio"
            type="radio"
            name="unit"
            id="imperial"
            value="imperial"
            @change="handleChecked"
          />
          <span class="checkmark"></span>
        </label>
      </div>

      <div class="values">
        <fieldset class="fieldset" :class="imperialClass">
          <legend class="legend">Height</legend>
          <label class="values__label" for="height">
            <input
              class="height-input"
              type="number"
              name="height"
              id="height"
              @input="handleChange"
              :data-type="dynamicIdHeight"
              placeholder="0"
              v-model="meterValue"
            />
            <span class="height-unit">{{ imperialClass ? 'ft' : 'm' }}</span>
          </label>
          <label class="values__label extra-value" for="inch">
            <input
              class="height-input"
              type="number"
              name="inch"
              id="inch"
              data-type="inch"
              @input="handleChange"
              placeholder="0"
              v-model="inchValue"
            />
            <span class="height-unit">in</span>
          </label>
        </fieldset>

        <fieldset class="fieldset" :class="imperialClass">
          <legend class="legend">Weight</legend>
          <label class="values__label" for="weight">
            <input
              class="weight-input"
              type="number"
              name="weight"
              id="weight"
              :data-type="dynamicIdWeight"
              @input="handleChange"
              placeholder="0"
              v-model="kiloValue"
            />
            <span class="weight-unit">{{ imperialClass ? 'st' : 'kg' }}</span>
          </label>
          <label class="values__label extra-value" for="lbs">
            <input
              class="weight-input"
              type="number"
              name="lbs"
              id="lbs"
              data-type="lbs"
              @input="handleChange"
              placeholder="0"
              v-model="lbsValue"
            />
            <span class="weight-unit">lbs</span>
          </label>
        </fieldset>
      </div>
    </form>
  </div>
</template>

<style lang=""></style>
