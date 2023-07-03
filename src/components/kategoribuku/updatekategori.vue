<script>
import axios from 'axios';
import {ref} from 'vue';

const selByKodeKategori = 'http://localhost/pustaka-buku/selectbykodekategori.php';
const urlUpdate = 'http://localhost/pustaka-buku/updatekategori.php';

export default {
  data() {
    return {
      selectKategori: ref([]),
      updatekode_kategori: '',
      updatekategori: '',
    };
  },
  mounted() {
    this.getKategori();
    this.updateKategori();
  },
  methods: {
    getKategori() {
      axios
          .get(selByKodeKategori + '?kode_kategori=' + this.$route.params.kode_kategori)
          .then((resp) => {
            console.log(resp);
            this.selectKategori = resp.data;
            this.updatekode_kategori = this.selectKategori.kode_kategori;
            this.updatekategori = this.selectKategori.kategori;
          })
          .catch((err) => {
            console.log(err);
          });
    },

    updateKategori() {
      let formData = new FormData();

      formData.append('kode_kategori', this.$route.params.kode_kategori);
      formData.append('kategori', this.updatekategori);

      axios
          .post(urlUpdate, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then((resp) => {
            console.log(resp.data);
            this.getKategori();
          })
          .catch((err) => {
            console.log(err);
          });
    },
  },
};

</script>

<template>
  <div class="intro">
    <div>
      <div class="welcome">Update Kategori Buku Perpustakaan Digital</div>
    </div>

    <div class="modal-body">
      <input
          class="form-control"
          type="text"
          v-model="updatekode_kategori"
          placeholder="Kode Kategori"
          aria-label="default input example"/><br/>
      <input
          class="form-control"
          type="text"
          v-model="updatekategori"
          placeholder="Kategori"
          aria-label="default input example"/><br/>
      <button
          type="button"
          class="btn btn-primary me-3"
          v-on:click="updateKategori()">
        Update Kategori
      </button>
      <router-link
          to="/readallkategori"
          class="btn btn-secondary me-5">
        Back
      </router-link>
    </div>

    <hr>

    <footer class="text-black text-center pb-5">
      <p>&copy; 2023 <a href="#" class="text-black fw-bold">Perpustakaan Digital</a> &middot; Created by Fitri
        Amalia</p>
    </footer>
  </div>

</template>

<style scoped>
.intro {
  padding-left: 300pt;
  padding-right: 300pt;
  background-color: #D3D3D3;
}

.welcome {
  font-size: 20pt;
  text-align: center;
  padding-top: 10pt;
  font-weight: bold;
  padding-bottom: 20pt;
}

</style>