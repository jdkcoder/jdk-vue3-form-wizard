# Installation

    npm i

    npm run dev

# Usage

Create the file **setIndex.js** in **src** folder

    import { ref } from  'vue';
    let index = ref(1)
    export { index }

import `{ index }` from **setIndex.js**  to **Wizard.vue** & **App.vue**

    import { index } from  './setIndex'

import `Wizard.vue` & `validate` function to **App.vue**

  

    <template>
	    <Wizard v-slot="{ index }" :steps="steps.value" :validate-function="validate()">
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
    import { index } from  './setIndex';
    import  Wizard  from  './Wizard.vue';
    
    let indexStep = ref(0);
    
    let steps = reactive([{
	    index:  indexStep++,
	    name:  'Products Source'
    },
    {
	    index:  indexStep++, 
	    name:  'Add Products'
    },
    {
	    index:  indexStep++,
	    name:  'Customer Info'
    },
    {
	    index: indexStep++,
	    name: 'Review Order'
    }])
    
    function validate() {
    	if (index.value > 1) {
    		alert('1')
    	}
    }
    </script>

## CSS Variables

    --jdk-fw-radius
    --jdk-fw-border
    --jdk-fw-border-width
    --jdk-fw-border-type
    --jdk-fw-border-clr
    --jdk-fw-padding
    
    --active-bg
    --active-border-clr
    --active-step-name-clr
    --active-step-num-clr
    --active-step-name-clr
    
    --unactive-bg
    --unactive-border-clr
    --unactive-step-num-clr
    --unactive-step-name-clr
    
    --nth-step-size
    
    --seperator-size
    --seperator-radius
    --seperator-clr
    --seperator-margin-y
    --seperator-margin-x
	
	--footer-btn-bg
	--back-btn-bg
	--back-btn-bg-hover
	--next-btn-bg
	--next-btn-bg-hover
    
    
    
