<template>
    <form @submit.prevent="handleSubmit">

        <ErrorComponent v-if="error" :error="error" />

        <h3>Вход в личный аккаунт</h3>

        <div class="form-group">
            <!-- <label>Email</label> -->
            <input type="text" class="form-control" v-model="email" placeholder="Email"/>
        </div>

        <div class="form-group">
            <!-- <label>Пароль</label> -->
            <input type="password" class="form-control" v-model="password" placeholder="Пароль"/>
        </div>

        <button class="btn btn-primary btn-block" style="margin: 15px">Войти</button>
    </form>
</template>

<script>
    import axios from 'axios'
    import ErrorComponent from './ErrorComponent.vue'
    export default {
        name: 'LoginComponent',

        components: {
            ErrorComponent
        },

        data() {
            return {
                email: '',
                password: '',
                error: ''
            }
        },
        methods: {
            async handleSubmit(){
                try{
                const response = await axios.post('authenticate', {
                    email: this.email,
                    password: this.password
                });

                console.log(response.data.jwttoken);
                console.log(this.email);
                console.log(this.password);
                localStorage.setItem('token', response.data.jwttoken);

                // this.$router.push('/');
                window.location.replace('/');
            } catch (e){
                window.scrollTo(0,0);
                this.error = 'Неверный email или пароль'
            }
            } 
        }
    }
</script>
