<template>
    <div class="card">
        <h3 class="card-header text-center">Register Area</h3>
        <div class="card-body">
            <form>
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <label>First Name</label>
                        <!--
                        $v = validation STATE
                        grabs properties from data object below
                        $v.firstname
                        $v.lastname
                        ...

                        -->
                        <!--
                            https://www.youtube.com/watch?v=SW5OfTAxtDY
                        4:17 of 14:49	Vuelidate (Form Validation) with Vue.js
                        -->
                        <input type="text" class="form-control" 
                            v-model.trim="$v.firstname.$model" :class="{
                            'is-invalid' :$v.firstname.$error,
                            'is-valid':!$v.firstname.$invalid }">                            
                            <div class="valid-feedback">Your first name is valid !</div>                               
                            <div class="invalid-feedback">
                                <span v-if="!$v.firstname.required">First name is required.</span>                                
                                <span v-if="!$v.firstname.minLength">First name must have at least {{
                                    $v.firstname.$params.minLength.min }} letters.</span>                                
                                <span v-if="!$v.firstname.maxLength">First name must have at most {{
                                    $v.firstname.$params.maxLength.max }} letters.</span>
                            </div>                               
                    </div>
                </div>
            </form>
        </div>

    </div>
    
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
