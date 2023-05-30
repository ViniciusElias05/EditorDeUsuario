<template>
    <div>
        <h2>Registro de usuário!</h2>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if=" error != undefined">
                    <div class="notification is-danger">
                        {{error}}
                    </div>
                </div>
                <label>Nome</label>
                <input type="text" placeholder="Nome do usuário" class="input" v-model="name">
                <label>E-mail</label>
                <input type="email" placeholder="email@email.com" class="input" v-model="email">
                <label >Senha</label>
                <input type="password" placeholder="******" class="input" v-model="password">
                <hr>
                <button class="button is-success" @click="register">Cadastrar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    data(){
        return{
            name: "",
            password: "",
            email: "",
            error: undefined
        }
    },
    methods: {

        register(){
            axios.post("http://localhost:8686/user",{
                name: this.name,
                password: this.password,
                email: this.email
            }).then( res =>{
                console.log(res);
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