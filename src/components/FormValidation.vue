<template>
    
</template>

<script>

import { required, minlength, maxlength, between } from 'vuelidate/lib/validators'

export default {
    
    name: 'FormValidation',
    // add state data method
    data() {  
            return {    // have it return an object
                        // different state properties
                        // '' = null
                firstname: '',
                lastname: '',
                age: 0                

            }
    },
    validations: {
        firstname: {
            required,
            minLength: minLength(3),
            maxLength: maxLength(10)
        },
        lastname: {
            minLength: minLength(5),
            maxLength: maxLength(12)
        },
        age: {
            between: between(15,40)

        }
    }
    
}
</script>

<!-- apply styles ONLY to this file -->
<style scoped>
</style>
