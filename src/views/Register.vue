<template>
    <div class="home">
        <h1>Cadastro de Usuários</h1>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <p>Nome</p>
                <input type="text" placeholder="Nome de usuário" class="input" v-model="name">
                <p>E-mail</p>
                <input type="email" placeholder="email@email.com" class="input" v-model="email">
                <p>Senha</p>
                <input type="password" placeholder="*****" class="input" v-model="password">
                <p>Cargo</p>
                <div class="control">
                    <div class="select">
                        <select class="is-hovered" v-model="role">
                            <option>Selecione um cargo</option>
                            <option value="0">Administrador</option>
                            <option value="1">Usuário</option>
                        </select>
                    </div>
                </div>
                <hr>
                <button class="button is-success" @click="register">Cadastrar</button>
            </div>
        </div>
    </div> 
</template>

<script>
export default {
    data(){
        return {
            name: "",
            password: "",
            email: "",
            role: ""
        }
    },
    methods:{
        register(){
            console.log(this.email);
            console.log(this.name);
            console.log(this.password);
            console.log(this.role);
        }
    }
}
</script>

<style scoped>

</style>