<template>
  <h1>JDK's Vue.js 3 Form Wizard</h1>

  <Wizard v-slot="{ index }" :validate-function="validate()">
    <div v-if='index === 1'>
      <label>
        <input v-model="orderFrom" value="1" type="radio" name="test" />
        Amazon
      </label>
      <label>
        <input v-model="orderFrom" value="2" type="radio" />
        External
      </label>
    </div>
    <div v-if='index === 2'>
      Step {{ index }}'s content
    </div>
    <div v-if='index === 3'>
      Step {{ index }}'s content
    </div>
    <div v-if='index === 4'>
      Step {{ index }}'s content
    </div>
  </Wizard>

  <div id="credit"><a href="//github.com/jdkcoder">Joker Dark Knight</a> <span>-</span> <a href="//jdk.vn" target="_blank">wWw.JDK.VN</a></div>
</template>

<script setup>
import { index } from './setIndex'
import Wizard from './Wizard.vue';
let orderFrom = $ref(null)
function validate() {
  if (index.value > 1) {
    if (!orderFrom) {
      alert('Choose product source, first')
      index.value = 1
    }
  }
}
</script>