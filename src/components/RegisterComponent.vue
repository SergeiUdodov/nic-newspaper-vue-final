<template>
    <form @submit.prevent="handleSubmit">

        <ErrorComponent v-if="error" :error="error" />

        <h3>Регистрация нового пользователя</h3>

        <div class="form-group">
            <!-- <label>First Name</label> -->
            <input type="text" class="form-control" v-model="first_name" placeholder="Имя"/>
        </div>

        <div class="form-group">
            <!-- <label>Last Name</label> -->
            <input type="text" class="form-control" v-model="last_name" placeholder="Фамилия"/>
        </div>

        <div class="form-group">
            <!-- <label>Email</label> -->
            <input type="email" class="form-control" v-model="email" placeholder="Email"/>
        </div>

        <div class="form-group">
            <!-- <label>Password</label> -->
            <input type="password" class="form-control" v-model="password" placeholder="Пароль"/>
        </div>

        <button class="btn btn-primary btn-block" style="margin: 15px">Зарегистрироваться</button>
    </form>
</template>

<script>
import axios from 'axios'
import ErrorComponent from './ErrorComponent.vue'
    export default {
        name: 'RegisterComponent',

        components: {
            ErrorComponent
        },

        data(){
            return {
                first_name: null,
                last_name: null,
                email: null,
                password: null,
                error: ''
            }
        },
        methods: {
            async handleSubmit(){
                    try{
                const response = await axios.post('register', {
                    firstName: this.first_name,
                    lastName: this.last_name,
                    email: this.email,
                    password: this.password

                });
                
                console.log(response);
                this.$router.push('/login');

                } catch (e){
                    window.scrollTo(0,0);
                    this.error = 'Не все поля заполнены / email уже существует';
                }
            }
        }
    }
</script>
