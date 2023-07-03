<script>
import axios from 'axios';
import { ref } from 'vue';

const selByKodeBuku = 'http://localhost/pustaka-buku/selectbykodebuku.php';
const urlUpdate = 'http://localhost/pustaka-buku/updatebuku.php';

export default {
  data() {
    return {
      selectBuku: ref([]),
      updatekode_buku: '',
      updatekode_kategori: '',
      updatejudul: '',
      updatepengarang: '',
      updatepenerbit: '',
      updatetahun: '',
      updateharga: '',
    };
  },
  mounted() {
    this.getBuku();
    this.updateBuku();
  },
  methods: {
    getBuku() {
      axios
          .get(selByKodeBuku + '?kode_buku=' + this.$route.params.kode_buku)
          .then((resp) => {
            console.log(resp);
            this.selectBuku = resp.data;
            this.updatekode_buku = this.selectBuku.kode_buku;
            this.updatekode_kategori = this.selectBuku.kode_kategori;
            this.updatejudul = this.selectBuku.judul;
            this.updatepengarang = this.selectBuku.pengarang;
            this.updatepenerbit = this.selectBuku.penerbit;
            this.updatetahun = this.selectBuku.tahun;
            this.updateharga = this.selectBuku.harga;

          })
          .catch((err) => {
            console.log(err);
          });
    },

    updateBuku() {
      let formData = new FormData();

      formData.append('kode_buku', this.$route.params.kode_buku);
      formData.append('kode_kategori', this.updatekode_kategori);
      formData.append('judul', this.updatejudul);
      formData.append('pengarang', this.updatepengarang);
      formData.append('penerbit', this.updatepenerbit);
      formData.append('tahun', this.updatetahun);
      formData.append('harga', this.updateharga);

      axios
          .post(urlUpdate, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then((resp) => {
            console.log(resp.data);
            this.getBuku();
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
      <div class="welcome">Update Data Buku Perpustakaan Digital</div>
    </div>

    <div class="modal-body">
      <input
          class="form-control"
          type="text"
          v-model="updatekode_buku"
          placeholder="Kode Buku"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updatekode_kategori"
          placeholder="Kode Kategori"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updatejudul"
          placeholder="Judul"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updatepengarang"
          placeholder="Pengarang"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updatepenerbit"
          placeholder="Penerbit"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updatetahun"
          placeholder="Tahun"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="updateharga"
          placeholder="Harga"
          aria-label="default input example" /><br />
      <button
          type="button"
          class="btn btn-primary me-3"
          v-on:click="updateBuku()">
        Update Buku
      </button>
      <router-link
          to="/readallbuku"
          class="btn btn-secondary me-5">
        Back
      </router-link>
    </div>

    <hr>

    <footer class="text-black text-center pb-5">
      <p>&copy; 2023 <a href="#" class="text-black fw-bold">Perpustakaan Digital</a> &middot; Created by Fitri Amalia</p>
    </footer>
  </div>

</template>

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
  padding-bottom: 20pt;
}

</style>