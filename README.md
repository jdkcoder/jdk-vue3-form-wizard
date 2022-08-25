# Installation
- Clone / download this repository

```
npm i
npm run dev
```

# Usage
Create the file **setIndex.js** in **src** folder

```
import { ref } from 'vue';
let index = ref(1)
export { index }```


import `{ index }` from **setIndex.js** to **App.vue** or any your **.vue** file & **Wizard.vue** 

```
import { index } from './setIndex'```
------------
import `Wizard.vue` to **App.vue** or any your **.vue** file

    <template>
	    <Wizard v-slot="{ index }" :seperator="true" :steps="steps.value">
            <div v-if='index === 1'>
                Step {{ index }}'s content
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
    </template>
	
    <script setup>
    import { reactive, ref } from 'vue';
    
    import { index } from './setIndex';

    import Wizard from './Wizard.vue';
    
    let indexStep = ref(0);
    
    let steps = reactive([{
	    index: indexStep.value++,
	    name: 'Products Source'
    },
    {
	    index: indexStep.value++, 
	    name: 'Add Products'
    },
    {
	    index: indexStep.value++,
	    name: 'Customer Info'
    },
    {
	    index: indexStep.value++,
	    name: 'Review Order'
    }])
    </script>


------------

Validate every single step with `validate` function
- Eg: `:validate-function="#YOUR_VALIDATE_FUNCTION"`

```html
    <template>
	    <Wizard v-slot="{ index }" :validate-function="validate">
            <div v-if='index === 1'>
                <label>
                    <input v-model="orderFrom" value="1" type="radio" name="test" />
                        Amazon
                </label>
                <label>
                    <input v-model="orderFrom" value="2" type="radio" name="test"/>
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
    </template>
```
    
    <script setup>
    import { reactive, ref } from 'vue';
    import { index } from './setIndex';
    import Wizard from './Wizard.vue';

    function validate() {
        if (index.value > 1) {
            if (!orderFrom) {
                alert('Choose product source, first')
                index.value = 1
            }
        }
    }
    </script>


------------

Trigger function when complete
- Eg: `:complete-function="#YOUR_COMPLETE_FUNCTION"`

```html
   <template>
	    <Wizard v-slot="{ index }" :complete-function="wizardCompleted">
            <div v-if='index === 1'>
                <label>
                    <input v-model="orderFrom" value="1" type="radio" name="test" />
                        Amazon
                </label>
                <label>
                    <input v-model="orderFrom" value="2" type="radio" name="test"/>
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
    </template>
    
    <script setup>
    import { reactive, ref } from 'vue';
    import { index } from './setIndex';
    import Wizard from './Wizard.vue';

    function wizardCompleted() {
        alert('completed')
    }
    </script>```
## CSS Variables
```
--jdk-fw-max-width
--jdk-fw-width
--jdk-fw-height
--jdk-fw-radius
--jdk-fw-border
--jdk-fw-border-width
--jdk-fw-border-type
--jdk-fw-border-clr
 --jdk-fw-padding

--nth-step-unactive-bg
--nth-step-active-bg
--nth-step-unactive-border-clr
--nth-step-active-border-clr
--nth-step-size

--unactive-step-name-clr
--active-step-name-clr

--sprt-size
--sprt-radius
--sprt-clr
--sprt-margin
--sprt-margin-top
--sprt-margin-right
--sprt-margin-bottom
--sprt-margin-left

--content-margin-bottom

--footer-btn-bg
--back-btn-bg
--back-btn-bg-hover
--next-btn-bg
--next-btn-bg-hover
--footer-btn-padding
--footer-btn-radius
-footer-btn-font-size
--footer-btn-font-weight```