<template>
    <div class="home">
        <h1>Login</h1>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="erro != undefined">
                    <div class="notification is-danger">
                        <p>{{erro}}</p>
                    </div>
                </div>
                <p>E-mail</p>
                <input type="email" placeholder="email@email.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" placeholder="*****" class="input" v-model="password">
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
        return {
            password: "",
            email: "",
            erro: undefined
        }
    },
    methods:{
        login(){
            axios.post("http://localhost:8686/login",{
                password: this.password,
                email: this.email
            }).then(res => {
                console.log(res);
                localStorage.setItem('token', res.data.token);
                this.$router.push({name:'Home'});
            }).catch(err => {
                var msgErro = err.response.data.err;
                this.erro = msgErro;
            })
        }
    }
}
</script>

<style scoped>

</style>