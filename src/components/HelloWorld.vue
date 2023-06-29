

<template>
  <html lang="pt-br">

  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
      integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
      crossorigin="anonymous" referrerpolicy="no-referrer" />
    <title>Login</title>
  </head>

  <body>
    <NavBar />
    <header>
      <nav class="content-header">
        <a href="#">
          <h3>João<span>Henryque</span></h3>
        </a>
        <router-link to="/login"><button>Login</button></router-link>
      </nav>
      <div class="text">
        <h1>Blog do J.<span>H</span></h1>
        <p>Tudo sobre Inteligência Artificial</p>
      </div>
    </header>
    <h1 class="card " style="text-align: center;">Lista de Usuários</h1>

    <div class="container mt-3">
      <div class="row justify-content-end">
        <div class="col-md-4">
          <div class="input-group">

            <input type="text" class="form-control" placeholder="Buscar usuário" v-model="searchQuery" @input="searchUsers">
            <button class="btn btn-primary" @click="resetSearch">Buscar</button>

          </div>
        </div>
      </div>
    </div>

    <div class="container mt-5 d-flex justify-content-between mx-auto table-scroll movel">
      <table class="table table-responsive">
        <thead class="table-dark">
          <tr class="align-middle">
            <th scope="col" class="text-bg-secondary card fs-1 text-dark text-align-center">id</th>
            <th scope="col" class="rounded border-0">Nome</th>
            <th scope="col" class="rounded border-0">Endereço</th>
            <th scope="col" class="rounded border-0">Idade</th>
            <th scope="col" class="rounded border-0">Telefone</th>
            <th scope="col" class="rounded border-0">Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id" class="align-middle">
            <th scope="row" class="text-bg-secondary card mt-2">{{ user.id }}</th>
            <td class="border-bottom border-2 text-uppercase lista">{{ user.nome }}</td>
            <td class="border-bottom border-2 text-uppercase lista">{{ user.endereco }}</td>
            <td class="border-bottom border-2 text-uppercase lista">{{ user.idade }}</td>
            <td class="border-bottom border-2 text-uppercase lista">{{ user.telefone }}</td>
            <td class="border-bottom border-2 d-inline-flex align-items-center gap-2">
              <button type="button" class="btn btn-sm btn-primary d-inline-flex align-items-center gap-2"
                @click="editUser(user)"><i class="fa-solid fa-pen-to-square" style="color: #4704ff;"></i>Editar</button>
              <button type="button" class="btn btn-sm btn-danger d-inline-flex align-items-center gap-2"
                @click="deleteUser(user.id)"><i class="fa-solid fa-trash" style="color: #ff0000;"></i>Deletar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <FormUpdate :selectedUser="selectedUser" v-if="selectedUser !== null" @updateUser="updateUser" />

  </body>

  </html>
</template>

<script>
import NavBar from '../components/NavBar.vue'
import FormUpdate from '../components/FormUpdate.vue'
import { RouterLink } from 'vue-router';
export default {
  components: {
    "router-link": RouterLink,
    NavBar,
    FormUpdate,
  },
  data() {
    return {
      users: [],
      selectedUser: null,
      showModal: false,
      searchQuery: '',
    };
  },
  mounted() {
    this.fetchUsers();
    this.searchUsers();
  },
  methods: {
    fetchUsers() {
      fetch('http://localhost:8000/api/users')
        .then(Response => Response.json())
        .then(data => {
          this.users = data;
        })
        .catch(error => {
          console.error('Erro ao buscar os usuários:', error);
        });
    },

    searchUsers() {
      if (this.searchQuery !== '') {
      const query = this.searchQuery.toLowerCase();
      this.users = this.users.filter(user => {
        const nome = user.nome.toLowerCase();
        const endereco = user.endereco.toLowerCase();
        const idade = user.idade.toString();
        const telefone = user.telefone.toString();

        return (
          nome.includes(query) ||
          endereco.includes(query) ||
          idade.includes(query) ||
          telefone.includes(query)
        );
      });
    }else {
      this.fetchUsers();
    }
  },

  resetSearch() {
  this.searchQuery = '';
  this.fetchUsers();
},

    editUser(user) {
      this.selectedUser = user;
      this.showModal = true;
    },
    closeModal() {
      this.selectedUser = null;
      this.showModal = false;
    },
    updateUser(updatedUser) {
      const index = this.users.findIndex(user => user.id === updatedUser.id);
      if (index !== -1) {
        this.users[index] = { ...updatedUser };
      }
      this.closeModal();
      alert('Usuário atualizado com sucesso');
    },

    deleteUser(userId) {
      // Envia uma solicitação DELETE para a API para excluir o usuário com o ID fornecido
      fetch(`http://localhost:8000/api/users/${userId}`, {
        method: 'DELETE'
      })
        .then(response => {
          if (response.ok) {
            // Remove o usuário excluído da lista local
            this.users = this.users.filter(user => user.id !== userId);
            alert('Usuário excluído com sucesso');
          } else {
            console.error('Erro ao excluir usuário:', response.status);
            alert('Erro ao excluir usuário');
          }
        })
        .catch(error => {
          console.error('Erro ao excluir usuário:', error);
          alert('Erro ao excluir usuário');
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
  height: 100%;
}

.table-scroll {
  max-height: 350px;
  /* Defina a altura máxima que desejar */
  overflow-y: auto;
  /* Adicione uma barra de rolagem vertical quando necessário */
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

.login {
  display: flex;
  margin: 10px auto;
  font-size: 15px;
  padding: 10px;
  border: none;
  border-radius: 5px;
  color: #c5c5c5;
  background-color: #000;
  cursor: pointer;
}

a {
  text-decoration: none;
}

.cadastro {
  text-align: center;
  font-size: 20px;
}

.cadastro button {
  border: none;
  font-size: 15px;
  padding: 7px;
  border-radius: 5px;
  color: #fff;
  background-color: #000;
  cursor: pointer;
}

header {
  height: 250px;
  background-color: #333;
}

.content-header h3 {
  font-size: 26px;
  color: #fff;
}

.content-header h3 span {
  color: rgb(0, 255, 170);
}

.content-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 900px;
  margin: 0 auto;
  padding: 20px;
}

button {
  color: #000;
  font-size: 20px;
  border: none;
  background-color: rgb(182, 182, 182);
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #000;
  color: #fff;
  border: 2px solid #fff;
  transform: scale(1.1);
  transition: 0.3s;
  border-radius: 25px 10px;
}

.text {
  text-align: center;
  color: #fff;
  margin-top: 10px;
}

.text h1 {
  font-size: 60px;
  margin-bottom: 20px;
}

.text h1 span {
  color: rgb(0, 255, 170);
}

.text p {
  font-size: 20px;

}</style>
