<template>
    <div class="card">
        <h3 class="card-header text-center">Register Area</h3>        
        <div class="card-body">
            <form>
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <label>First Name</label>
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
                    <div class="form-group col-md-6">
                        <label>Last Name</label>
                        <input type="text" class="form-control" 
                            v-model.trim="$v.lastname.$model" 
                            :class="{ 'is-invalid' :$v.lastname.$error,
                            'is-valid':!$v.lastname.$invalid }">                            
                            <div class="valid-feedback">Your last name is valid !</div>                               
                            <div class="invalid-feedback">
                                <span v-if="!$v.lastname.required">Last name is required.</span>                                
                                <span v-if="!$v.lastname.minLength">Last name must have at least {{
                                    $v.lastname.$params.minLength.min }} letters.</span>                                
                                <span v-if="!$v.lastname.maxLength">Last name must have at most {{
                                    $v.lastname.$params.maxLength.max }} letters.</span>
                            </div>                               
                    </div>                    
                </div>
                <div class="form-group">
                    <label>Age</label>
                    <input type="number" class="form-control" 
                        v-model.number.lazy="$v.age.$model" 
                        :class="{
                        'is-invalid' :$v.age.$error,
                        'is-valid':!$v.age.$invalid }">                            
                        <div class="valid-feedback">Your age is valid !</div>                               
                        <div class="invalid-feedback">
                            <span v-if="!$v.age.between"> 
                                Must be between 
                                {{$v.age.$params.between.min}} and 
                                {{$v.age.$params.between.max}}                            
                            </span>
                        </div>                               
                </div>
            </form>
        </div>

    </div>
    
</template>

<script>

import { required, minLength, maxLength, between, email } from 'vuelidate/lib/validators'

export default {
    
    name: 'FormValidation',
    // add state data method
    data() {  
            return {    // have it return an object
                        // different state properties
                        // '' = null
                firstname: '',
                lastname: '',
                username: '',
                email: ''
            }
    },
    validations: {
        firstname: {
            required,
            minLength: minLength(3),
            maxLength: maxLength(10)
        },
        lastname: {
            /*
            if you do NOT set 
            required,
                Your last name is valid !
            will appear when the form is loaded with NO value in it
            */
            minLength: minLength(5),
            maxLength: maxLength(12)
        },
        username: {
            required,
            isUnique(value) {
                if (value === '') return true
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(typeof value === 'string' && value.length % 2 !== 0)
                    }, 350 + Math.random() * 300)                      

                })        
            }
        },
        email: {
            required,
            email,
            isUnique(value) {
                if (value === '') return true
                /*
                https://stackoverflow.com/questions/53592444/regex-rule-for-email-validation-is-not-working-in-vuejs
                regex rule for email validation is not working in vuejs
                */
                // eslint-disable-next-line
                var email_regex = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

                //var email_regex = /^(([]
                /*
                    todo
                add EMAIL reg expresion later
                7:31 of 14:49
                in tutorial
                https://www.youtube.com/watch?v=SW5OfTAxtDY
                */    
                return new Promise((resolve) => {
/*                    
                    setTimeout(() => {
                        resolve(typeof value === 'string' && value.length % 2 !== 0)
                    }, 350 + Math.random() * 300)                      
*/
                    setTimeout(() => {
                        resolve(email_regex.test(value))
                    }, 350 + Math.random() * 300)                      



                })        
            }
        }
    }
    
}
</script>

<!-- apply styles ONLY to this file -->
<style scoped>
</style>
