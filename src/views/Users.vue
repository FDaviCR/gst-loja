<template>
    <div class="wrapper">
        <h1>Painel Adm!</h1>
        <hr>
        <div class="columns is-centered">
            <table class="table">
                <thead>
                    <tr>
                        <th>Nome</th>
                        <th>E-mail</th>
                        <th>Cargo</th>
                        <th>Ações</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="user in users" :key="user.id">
                        <td>{{user.name}}</td>
                        <th>{{user.email}}</th>
                        <td>{{ user.role | processRole}}</td>
                        <th>
                            <button class="button is-success">Editar</button>
                            <button class="button is-danger" @click="showDeleteModal(user.id)">Deletar</button>
                        </th>
                    </tr>
                </tbody>
            </table>

            <div :class="{modal: true, 'is-active': showModal}">
                <div class="modal-background"></div>
                <div class="modal-content">
                    <div class="card">
                        <header class="card-header">
                            <p class="card-header-title">
                                Deletar
                            </p>
                            <a href="#" class="card-header-icon" aria-label="more options">
                            <span class="icon">
                                <i class="fas fa-angle-down" aria-hidden="true"></i>
                            </span>
                            </a>
                        </header>
                        <div class="card-content">
                            <div class="content">
                                Você quer mesmo deletar o usuário?  
                            </div>
                        </div>
                        <footer class="card-footer">
                            <a href="#" class="card-footer-item" @click="hideModal()">Cancelar</a>
                            <a href="#" class="card-footer-item" @click="deleteUser()">Sim, desejo deletar</a>
                        </footer>
                    </div>
                </div>
                <button class="modal-close is-large" aria-label="close" @click="hideModal()"></button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    created(){
        var req = {
            headers: {
                Authorization: "Bearer" + localStorage.getItem('token')
            }
        }

        axios.get('http://localhost:8686/user', req).then(res => {
            this.users = res.data;
        }).catch(err => {
            console.log(err)
        })
    },
    data(){
        return {
            users: [],
            showModal: false,
            deleteUserId: -1
        }
    },
    methods:{
        hideModal(){
            this.showModal = false;
        },
        showDeleteModal(id){
            this.showModal = true;
            this.deleteUserId = id;
        },
        deleteUser(){

            var req = {
                headers: {
                    Authorization: "Bearer " + localStorage.getItem('token')
                }
            }
            axios.delete("http://localhost:8686/user/"+this.deleteUserId, req).then(res => {
                console.log(res);
                this.showModal = false;
                axios.get('http://localhost:8686/user', req).then(res => {
                    this.users = res.data;
                }).catch(err => {
                    console.log(err)
                })
            }).catch(err => {
                this.showModal = false;
                console.log(err);
            })
        }
    },
    filters:{
        processRole: function(value){
            if(value == 0){
                return "Administrador";
            }else if(value == 1){
                return "Usuário";
            }
        }
    }
}
</script>

<style scoped>
.wrapper{
	height: 100vh;
	width: 100vw;
	background-color: #34495e;
	color: #fff;
}
</style>