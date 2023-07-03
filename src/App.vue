<template>

  <div class="intro">
    <!--Navigation Bar-->
    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">Perpustakaan Digital</a>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
            <div class="navbar-nav">
              <a class="nav-link active" aria-current="page"> <router-link to="/" style="text-decoration: none" class="btn">Home</router-link></a>
              <a class="nav-link"> <router-link to="/readallbuku" style="text-decoration: none" class="btn">Data Buku</router-link></a>
              <a class="nav-link"> <router-link to="/readallkategori" style="text-decoration: none" class="btn">Kategori Buku</router-link></a>
            </div>
          </div>
        </div>
      </nav>
  </div>

  <!--Router View-->
  <RouterView/>

</template>

<style scoped>
.intro {
  padding-left: 100pt;
  padding-right: 100pt;
}

.container-fluid {
  font-size: 14pt;
}

.navbar-brand {
  font-weight: bold;
  font-style: oblique;
}

</style>
