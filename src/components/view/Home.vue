<template>

  <div class="intro">
    <div>
      <div class="welcome">SELAMAT DATANG DI PERPUSTAKAAN DIGITAL</div>
    </div>

    <div class="background">
      <div class="image">
        <img src="@/assets/perpustakaan.jpg" alt=" "
             height="400" width="1050" />
      </div>

      <div>
        <div class="ringkasan">Perpustakaan digital atau digital library menawarkan kemudahan bagi para pengguna untuk mengakses sumber-sumber elektronik dengan alat yang menyenangkan pada waktu dan kesempatan yang terbatas. Perpustakaan digital adalah suatu perpustakaan yang menyimpan data baik itu buku (tulisan), gambar, suara dalam bentuk elektronik dan mendistribusikannya dengan menggunakan protokol elektronik melalui jaringan komputer.</div>
      </div>

      <hr>

      <footer class="text-black text-center pb-5">
        <p>&copy; 2023 <a href="#" class="text-black fw-bold">Perpustakaan Digital</a> &middot; Created by Fitri Amalia</p>
      </footer>
    </div>
  </div>

</template>

<script>
export default {
  name: "Home"
}
</script>

<style scoped>

.intro {
  padding-left: 100pt;
  padding-right: 100pt;
  background-color: #D3D3D3;
}

.welcome {
  font-size: 20pt;
  text-align: center;
  padding-top: 10pt;
  font-weight: bold;
  background-color: #D3D3D3;
  padding-bottom: 10pt;
}

.image {
  text-align: center;
  padding-top: 5px;
  padding-bottom: 10px;
}

.ringkasan {
  padding-left: 50pt;
  padding-right: 50pt;
  padding-top: 10pt;
  padding-bottom: 5pt;
  font-size: 15pt;
  text-align: justify;
}

</style>