<template>
    <div>
        <v-container>
            <v-row>
                <v-col>
                    <h1>Singup</h1>
                    <v-form ref="singUpForm" v-model="formValidity">
                        <v-text-field 
                        label="Enter email"
                        v-model="email"
                        :rules="emailRules"
                        required
                        ></v-text-field>

                        <v-autocomplete 
                            label="Which browser do you use?" 
                            :items="browsers"
                        ></v-autocomplete>

                        <v-file-input
                          accept="image/*"
                          label="File input"
                        ></v-file-input>

                        <v-text-field v-model="picker" readonly></v-text-field>
                        <div class="row" justify="left">
                            <v-date-picker v-model="picker"></v-date-picker>
                        </div>
                        
                        <v-checkbox
                          v-model="agreeToTerms"
                          label="Agree terms & conditions."
                          color="red"
                          :rules="agreeToTermsRules"
                          required
                        ></v-checkbox>

                        <v-btn class="mr-4" color="primary" :disabled="!formValidity">Sing Up</v-btn>
                        <v-btn class="mr-4" color="success" @click="formValidate">Validate Form</v-btn>
                        <v-btn class="mr-4" @click="resetValidation()" color="warning">Reset Validation</v-btn>
                        <v-btn @click="reset" color="error">Reset</v-btn>
                    </v-form>
                </v-col>
            </v-row>
        </v-container>
    </div>
</template>

<script>
    export default {
        data: () => ({
            browsers: ['Chrome','Firefox','Safari','Opera','Internet Explore'],
            picker: '',
            agreeToTerms: false,
            agreeToTermsRules: [
                value => !!value || 'You must agree terms and conditions to sing up for an account.'
            ],
            email: '',
            emailRules: [
                value => !!value || 'Required email address.',
                value => value.indexOf('@') !== 0 || 'Email should have a username.',
                value => value.includes('@') || 'Email should have a @ simbol.',
                value => value.indexOf('.') - value.indexOf('@') > 1 || 'Email should have a domain.',
                value => value.indexOf('.') <= value.length - 3 || 'Email should contain a valid domain extension.'
            ],
            formValidity: false
        }),
        methods: {
            resetValidation(){
                this.$refs.singUpForm.resetValidation()
            },
            reset(){
                this.$refs.singUpForm.reset()
            },
            formValidate(){
                this.$refs.singUpForm.validate()
            }
        }
    }
</script>

<style scoped>

</style>