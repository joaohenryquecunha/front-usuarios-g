<template>
    
    <div class="content">
      <div id="cadastro" class="card">
        <form >
          <h1>Cadastro</h1>
          <hr><br>
          <p>
            <label for="nome">Nome</label>
            <input class="border-bottom border-dark border-3" type="text" v-model="selectedUser.nome" required>
          </p>
          <p>
            <label for="endereco">Endereço</label>
            <input class="border-bottom border-dark border-3" type="endereco" v-model="selectedUser.endereco" required>
          </p>
          <p>
            <label for="idade">Idade</label>
            <input class="border-bottom border-dark border-3" type="number" v-model="selectedUser.idade" required>
          </p>
          <p>
            <label for="telefone">Telefone</label>
            <input class="border-bottom border-dark border-3" type="tel" v-model="selectedUser.telefone" required>
          </p>
          <button type="button" @click="updateUser">Salvar</button>
          <hr><br>
        </form>
        
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      selectedUser: {
        type: Object,
        required: true
      }
    },
    methods: {
      updateUser() {
        fetch(`http://localhost:8000/api/users/${this.selectedUser.id}`, {
          method: 'PUT',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(this.selectedUser)
        })
        .then(response => response.json())
        .then(data => {
          console.log('Usuário atualizado:', data);
        })
        .catch(error => {
          console.error('Erro ao atualizar usuário:', error);
        });
      }
    }
  }
  </script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    font-family: Arial, Helvetica, sans-serif;
}

body {
    margin: 0 auto;
}

.content {
    display: flex;
    justify-content: center;
    margin-top: 20px;
    margin-bottom: 10px;
}

.card {
    border: 2px solid;
    padding: 55px;
    background: linear-gradient(90deg,rgb(21, 255, 0),rgb(113, 199, 159));
    border-radius: 50px 0px;
    filter: drop-shadow(15px 20px 10px rgb(0, 0, 0));
}

form h1 {
    text-align: center;
    margin-bottom: 20px;
    font-size: 50px;
}

form input {
    padding: 5px;
    margin: 10px auto;
    width: 220px;
    background-color: rgb(199, 199, 199);
    border: none;
    border-radius: 5px;
}

form label {
    display: flex;
}

a {
    text-decoration: none;
}

header {
    height: 250px;
    background-color: #333;
}


button {
    color:#fff;
    font-size: 20px;
    border: none;
    background-color:#000;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    display: flex;
    justify-content:end;
}

button:hover {
    background-color: #000;
    color: #fff;
    transform: scale(1.1);
    transition: 0.3s;
    border-radius: 25px 10px;
    border: 2px solid #fff;
}

</style>
  