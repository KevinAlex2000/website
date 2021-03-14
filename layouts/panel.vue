<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">
          <logo width="30px" height="30px" dark="true" />
        </a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mb-2 mb-lg-0 ms-auto">
            <li class="nav-item">
              <a class="nav-link active" href="#">Inicio</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Curriculum</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Perfil web</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Cerrar sesión</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div class="container">
      <Nuxt />
    </div>
  </div>
</template>
