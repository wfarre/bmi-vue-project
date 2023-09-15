<script setup lang="ts">
import HeaderVue from './components/Header/HeaderVue.vue'
import SectionExplanation from './components/SectionExplanation.vue'
import SectionAdvice from './components/SectionAdvice/SectionAdvice.vue'

import { ref, watch } from 'vue'

// const bmi = ref(0)
</script>

<template>
  <HeaderVue />

  <main class="main">
    <SectionExplanation />
    <SectionAdvice />
    <section class="section section--limitations">
      <div class="decoration-img decoration-img--right">
        <img src="./assets/images/pattern-curved-line-right.svg" alt="" />
      </div>
      <header class="section__header">
        <h2 class="section__header__title">Limitations of BMI</h2>
        <p class="section__header__content">
          Although BMI is often a practical indicator of healthy weight, it is not suited for every
          person. Specific groups should carefully consider their BMI outcomes, and in certain
          cases, the measurement may not be beneficial to use.
        </p>
      </header>

      <div class="section__main">
        <div class="container">
          <div class="card card--limitation">
            <div class="card__header">
              <div class="icon-wrapper">
                <img src="./assets/images/icon-gender.svg" alt="" />
              </div>
              <h3 class="title">Gender</h3>
            </div>
            <div class="card__main">
              <p class="text">
                The development and body fat composition of girls and boys vary with age.
                Consequently, a child's age and gender are considered when evaluating their BMI.
              </p>
            </div>
          </div>

          <div class="card card--limitation">
            <div class="card__header">
              <div class="icon-wrapper">
                <img src="./assets/images/icon-age.svg" alt="" />
              </div>
              <h3 class="title">Age</h3>
            </div>
            <div class="card__main">
              <p class="text">
                In aging individuals, increased body fat and muscle loss may cause BMI to
                underestimate body fat content.
              </p>
            </div>
          </div>

          <div class="card card--limitation">
            <div class="card__header">
              <div class="icon-wrapper">
                <img src="./assets/images/icon-muscle.svg" alt="" />
              </div>
              <h3 class="title">Muscle</h3>
            </div>
            <div class="card__main">
              <p class="text">
                BMI may misclassify muscular individuals as overweight or obese, as it doesn't
                differentiate muscle from fat.
              </p>
            </div>
          </div>

          <div class="card card--limitation">
            <div class="card__header">
              <div class="icon-wrapper">
                <img src="./assets/images/icon-pregnancy.svg" alt="" />
              </div>
              <h3 class="title">Pregnancy</h3>
            </div>
            <div class="card__main">
              <p class="text">
                Expectant mothers experience weight gain due to their growing baby. Maintaining a
                healthy pre-pregnancy BMI is advisable to minimise health risks for both mother and
                child.
              </p>
            </div>
          </div>

          <div class="card card--limitation">
            <div class="card__header">
              <div class="icon-wrapper">
                <img src="./assets/images/icon-race.svg" alt="" />
              </div>
              <h3 class="title">Race</h3>
            </div>
            <div class="card__main">
              <p class="text">
                Certain health concerns may affect individuals of some Black and Asian origins at
                lower BMIs than others. To learn more, it is advised to discuss this with your GP or
                practice nurse.
              </p>
            </div>
          </div>
        </div>
      </div>

      <footer class="section__footer"></footer>
    </section>
  </main>
</template>

<style scoped></style>
