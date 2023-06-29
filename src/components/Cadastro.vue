<template>
  <NavBar/>
    <div class="content">
      <div id="cadastro" class="card">
        <form @submit="submitForm" method="post">
          <h1>Cadastro</h1>
          <hr><br>
          <p>
            <label for="nome">Nome</label>
            <input class="border-bottom border-dark border-3" type="text" v-model="nome" required>
          </p>
          <p>
            <label for="endereco">Endereço</label>
            <input class="border-bottom border-dark border-3" type="endereco" v-model="endereco" required>
          </p>
          <p>
            <label for="idade">Idade</label>
            <input class="border-bottom border-dark border-3" type="number" v-model="idade" required>
          </p>
          <p>
            <label for="telefone">Telefone</label>
            <input class="border-bottom border-dark border-3" type="tel" v-model="telefone" required>
          </p>
          <button type="submit" class="login">Cadastro</button>
          <hr><br>
        </form>
        <div class="cadastro">
          <span>Já tem conta?</span>
          <a href="/"><button>Login</button></a>
          
        </div>
      </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue';

const nome = ref('');
const endereco = ref('');
const idade = ref();
const telefone = ref('');

const submitForm = async (event) => {
  event.preventDefault();
  const formData = {
    nome: nome.value,
    endereco: endereco.value,
    idade: idade.value,
    telefone: telefone.value,
  };

  try {
    const response = await fetch('http://localhost:8000/api/users/', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData),
    });

    if (response.ok) {
      alert('Usuário cadastrado com sucesso!');
      nome.value = '';
      endereco.value = '';
      idade.value = null;
      telefone.value = '';
    } else {
      const errorMessage = await response.text();
      alert(`Erro ao cadastrar usuário: ${errorMessage}`);
    }
  } catch (error) {
    alert(`Erro ao realizar a requisição: ${error.message}`);
  }
};
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
    color: #fff;
    font-size: 20px;
    border: none;
    background-color: rgb(0, 255, 170);
    color: #000;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #333;
    color: #fff;
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
    color:rgb(0, 255, 170);
}

.text p {
    font-size: 20px;
}
</style>