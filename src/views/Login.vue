<template>
    <div class="wrapper">
        <div class="box">
            <h1>Login</h1>           
            <div class="boxIntern">
                <div class="column">
                    <div v-if="erro != undefined">
                        <div class="notification is-danger">
                            <button class="delete" @click="close"></button>
                            <p>{{erro}}</p>
                        </div>
                    </div>
                    <input type="email" placeholder="E-mail" v-model="email">
                    <input type="password" placeholder="Senha" v-model="password">
                    
                    <button class="button is-success is-outlined is-rounded" @click="login">Logar</button>
                </div>
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
        },
        close(){
            this.erro = undefined;
        }
    }
}
</script>

<style scoped>
.wrapper{
	height: 100vh;
	width: 100vw;
	background-color: #34495e;
	position: absolute;
	left: 0;
	top: 0;
	display: flex;
	align-items: center;
	justify-content: center;
	color: #fff;
	transition: .5s;
}
.box{
    width: 350px;
    height: 400px;
    padding: 20px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    background: rgba(0,0,0,0.5);
    text-align: center;
}
.boxIntern{
    padding-top: 50px;
}
.box h1{
  color: white;
  text-transform: uppercase;
  font-weight: 500;
}
.box input[type = "email"],.box input[type = "password"]{
  border:0;
  background: none;
  display: block;
  margin: 20px auto;
  text-align: center;
  border: 2px solid #3498db;
  padding: 14px 10px;
  width: 200px;
  outline: none;
  color: white;
  border-radius: 24px;
  transition: 0.25s;
}
.box input[type = "email"]:focus,.box input[type = "password"]:focus{
  width: 280px;
  border-color: #2ecc71;
}
.box .button{
  width: 200px;
  border:0;
  background: none;
  display: block;
  margin: 20px auto;
  text-align: center;
  border: 2px solid #2ecc71;
  outline: none;
  color: white;
  border-radius: 24px;
  transition: 0.25s;
  cursor: pointer;
}
::-webkit-input-placeholder {
   color: grey;
}

:-moz-placeholder { /* Firefox 18- */
   color: grey;
}

::-moz-placeholder {  /* Firefox 19+ */
   color: grey;
}

:-ms-input-placeholder {  
   color: grey;  
}

</style>