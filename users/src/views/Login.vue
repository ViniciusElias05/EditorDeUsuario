<template>
    <div>
        <h1>Login</h1>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if=" error != undefined">
                    <div class="notification is-danger">
                        {{error}}
                    </div>
                </div>
                <label>E-mail</label>
                <input type="email" placeholder="email@email.com" class="input" v-model="email">
                <label >Senha</label>
                <input type="password" placeholder="******" class="input" v-model="password">
                <hr>
                <button class="button is-success" @click="login">Logar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    data(){
        return{
            password: "",
            email: "",
            error: undefined
        }
    },
    methods: {

        login(){
                axios.post("http://localhost:8686/login",{
                password: this.password,
                email: this.email
            }).then( res =>{
                console.log(res);
                localStorage.setItem('token', res.data.token);
                this.$router.push({name: 'home'});
            }).catch(err =>{
                var msgErr = err.response.data.err;
                this.error = msgErr;
            });
        }
    }
}
</script>

<style scoped>

</style>