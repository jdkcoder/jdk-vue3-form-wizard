<template>
    <div id="form-wizard">
        <div id="steps">
            <button v-for="step in props.steps" @click="changeStep(step)" :class="{ active: index === step.index }" :index="step.index" :key="step.index">
                <p class="nth-step">{{ step.index }}</p>
                <span class="step-name">{{ step.name }}</span>
            </button>
        </div>
        <div class="seperator"></div>
        <div id="step-content">
            <slot :index="index" />
        </div>
        <div id="step-footer">
            <button @click="back" id="back">Back</button>
            <button @click="next" id="next">Next</button>
        </div>
    </div>
</template>

<script setup>
import { index } from './setIndex'
let props = defineProps({
    steps: {
        type: Array,
        default: () => [
            {
                index: 1,
                name: 'Products Source'
            },
            {
                index: 2,
                name: 'Add Products'
            },
            {
                index: 3,
                name: 'Customer Info'
            },
            {
                index: 4,
                name: 'Review Order'
            }
        ]
    },
    validateFunction: { type: Function }
})



function changeStep(step) {

    if (props.validateFunction) {
        props.validateFunction()
    }

    index.value = step.index
}

function next() {
    if (index.value <= 3) {
        index.value++
        if (props.validateFunction) {
            props.validateFunction()
        }

    } else {
        return false
    }
    console.log(index.value);
}

function back() {
    if (index.value !== 1) {
        index.value--
        if (props.validateFunction) {
            props.validateFunction()
        }
    }

    if (index.value === 1) {
        return 0
    }
}
</script>
