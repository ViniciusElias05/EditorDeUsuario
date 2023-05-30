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
                <hr>
                <button class="button is-success" @click="update">Editar</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    created(){
          var req = {
                headers:{
                    Authorization: "Bearer " + localStorage.getItem('token')
                }
            }
        axios.get("http://localhost:8686/user/" + this.$route.params.id,req).then(res =>{
            console.log(res);
            this.name = res.data.name;
            this.email = res.data.email;
            this.id = res.data.id;
        }).catch(err =>{
            console.log(err.response);
            this.$router.push({name: 'Users'});
        })
    },
    data(){
        return{
            name: "",
            email: "",
            id: -1,
            error: undefined
        }
    },
    methods: {
        

        update(){
             var req = {
                headers:{
                    Authorization: "Bearer " + localStorage.getItem('token')
                }
            }
            axios.put("http://localhost:8686/user",{
                name: this.name,
                email: this.email,
                id: this.id
            }, req).then( res =>{
                console.log(res);
                this.$router.push({name: 'Users'});
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