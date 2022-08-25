<template>
  <div
    id="form-wizard"
    :style="{ '--grid-rows: min-content 1fr min-content': !seperator }"
  >
    <div id="steps">
      <button
        v-for="step in props.steps"
        @click="changeStep(step)"
        :class="{ active: index === step.index }"
        :index="step.index"
        :key="step.index"
      >
        <p class="nth-step">{{ step.index }}</p>
        <span class="step-name">{{ step.name }}</span>
      </button>
    </div>
    <div class="jdk-fw-seperator" :class="{ hidden: !seperator }"></div>
    <div id="step-content">
      <slot :index="index" />
    </div>
    <div id="step-footer">
      <button @click="back" id="back">Back</button>
      <button v-if="index != props.steps.length" @click="next" id="next">Next</button>
      <button
        v-if="index == props.steps.length"
        @click="complete()"
        id="next"
      >
        Done
      </button>
    </div>
  </div>
</template>

<script setup>
import { index } from "./setIndex";
let props = defineProps({
  steps: {
    type: Array,
    default: () => [
      {
        index: 1,
        name: "Nguồn sản phẩm",
      },
      {
        index: 2,
        name: "Thêm sản phẩm",
      },
      {
        index: 3,
        name: "Thông tin khách hàng",
      },
    ],
  },
  validateFunction: { type: Function },
  completeFunction: { type: Function },
  seperator: { type: Boolean, default: true },
});

function changeStep(step) {
  if (props.validateFunction) {
    props.validateFunction();
  }

  index.value = step.index;
}

function next() {
  if (index.value < props.steps.length) {
    index.value++;
    if (props.validateFunction) {
      props.validateFunction();
    }
  } else {
    return false;
  }
  console.log(index.value);
}

function back() {
  if (index.value !== 1) {
    index.value--;
    if (props.validateFunction) {
      props.validateFunction();
    }
  }

  if (index.value === 1) {
    return 0;
  }
}

function complete() {
  if(props.completeFunction) {
    props.completeFunction()
  }
}
</script>
<style lang="sass?indentedSyntax">
@import '@/assets/styles/_form-wizard'
</style>
