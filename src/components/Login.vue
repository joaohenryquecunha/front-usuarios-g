<template>
    <html lang="pt-br">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <link rel="stylesheet" href="login.css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
</head>

<body>
    <NavBar/>
    <header>
        <nav class="content-header">
            <a href="index.html"><h3>João<span>Henryque</span></h3></a>
            <a href="./login.html"><button>Login</button></a>
        </nav>
        <div class="text">
            <h1>Blog do J.<span>H</span></h1>
            <p>Tudo sobre Inteligência Artificial</p>
        </div>
    </header>

    <div class="content">
        <div id="login" class="card">
            <form method="post" action="#">
                <h1>Login</h1>
                <hr><br>
                <p>
                    <label for="email_login">E-mail</label>
                    <input type="email" id="email_login" name="email_login">
                </p>
                <p>
                    <label for="senha_login">Senha</label>
                    <input type="password" id="senha_login" name="senha_login">
                </p>
                <a href="#"><button class="login">Longin</button></a>
                <hr><br>
            </form>
            <div class="cadastro">
                <span>Não tem cadastro?</span>
                <router-link to="/cadastro"><button>Cadastre-se</button></router-link>
            </div>
        </div>
    </div>
</body>

</html>
</template>

<script>
import { RouterLink } from 'vue-router';

export default {
  components: {
    'router-link': RouterLink
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
    padding: 15px;
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
    padding: 7px;
    border: none;
    border-radius: 5px;
    color: #000;
    background-color: #8a8a8a;
    cursor: pointer;
}

a {
    text-decoration: none;
}

.cadastro {
    text-align: center;
}

.cadastro button {
    border: none;
    font-size: 15px;
    padding: 3px;
    border-radius: 5px;
    color: #fff;
    background-image: linear-gradient(45deg, #333, #000);
    cursor: pointer;
}

header {
    height: 220px;
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
    background-color: rgb(0, 255, 170);;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #000;
    color: #fff;
    transform: scale(1.1);
    transition: 0.3s;
    border-radius: 25px 10px;
    border: 2px solid #fff;
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
}
</style>