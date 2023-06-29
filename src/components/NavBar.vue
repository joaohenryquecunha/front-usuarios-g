<template>
    <nav class="navbar navbar-dark bg-dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Lista de usuários</a>
      <button class="navbar-toggler btn btn-outline-success" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasDarkNavbar" aria-controls="offcanvasDarkNavbar">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="offcanvas offcanvas-end text-bg-dark" tabindex="-1" id="offcanvasDarkNavbar" aria-labelledby="offcanvasDarkNavbarLabel">
        <div class="offcanvas-header">
          <h5 class="offcanvas-title" id="offcanvasDarkNavbarLabel">Menu Blog</h5>
          <button type="button" class="btn-close btn-close-white" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body card-body">
          <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
            <li class="nav-item">
              <router-link to="/"><button type="button" class="btn btn-outline-secondary btn-sm container-fluid mb-1">Home</button></router-link>
            </li>
            <li class="nav-item">
                <router-link to="/login"><button type="button" class="btn btn-outline-secondary btn-sm container-fluid mb-1">Login</button></router-link>
            </li>
            <li class="nav-item">
                <router-link to="/cadastro"><button type="button" class="btn btn-outline-secondary btn-sm container-fluid mb-1">Cadastro</button></router-link>
            </li>
            <li class="nav-item">
                <router-link to="/"><button type="button" class="btn btn-outline-secondary btn-sm container-fluid mb-1">Lista de Usuários</button></router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>

</script>