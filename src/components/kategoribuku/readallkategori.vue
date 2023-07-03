<script>
import axios from 'axios';
import { ref } from 'vue';

const readAllKategori = 'http://localhost/pustaka-buku/readallkategori.php';
const insertKategori = 'http://localhost/pustaka-buku/insertkategori.php';
const delKategori = 'http://localhost/pustaka-buku/deletekategori.php';

export default {
  data() {
    return {
      kategori: ref([]),
      insertkode_kategori: '',
      insertkategori: '',
    };
  },
  mounted() {
    this.readKategori();
  },
  methods: {
    readKategori() {
      axios
          .get(readAllKategori)
          .then((resp) => {
            console.log(resp);
            this.kategori = resp.data;
          })
          .catch((err) => {
            console.log(err);
          });
    },

    postKategori() {
      let formData = new FormData();

      formData.append('kode_kategori', this.insertkode_kategori);
      formData.append('kategori', this.insertkategori);

      axios
          .post(insertKategori, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then((resp) => {
            console.log(resp.data);
            this.readKategori();
            this.insertkode_kategori = '';
            this.insertkategori = '';
          })
          .catch((err) => {
            console.log(err);
          });
    },

    deleteKategori(kode_kategori) {
      if (confirm('Apakah Anda yakin ingin menghapus kategori buku?')) {
        axios
            .get(delKategori + '?kode_kategori=' + kode_kategori)
            .then((resp) => {
              console.log(resp);
              this.readKategori();
            })
            .catch((err) => {
              console.log(err);
            });
      }
    },
  },
};
</script>

<template>
  <div class="intro">
    <div>
      <div class="welcome">Daftar Kategori Buku Perpustakaan Digital</div>
    </div>

    <thead>
    <tr>
      <td class="border" style="text-align: center;width: 400px"><strong>Kode Kategori</strong></td>
      <td class="border" style="text-align: center;width: 400px"><strong>Kategori</strong></td>
      <td class="border" style="text-align: center;width: 400px"><strong>Aksi</strong></td>
    </tr>
    </thead>
    <tbody>
    <tr v-for="data in kategori">
      <td>{{ data.kode_kategori }}</td>
      <td>{{ data.kategori }}</td>
      <td>
        <router-link
            :to="{ name: 'updatekategori', params: { kode_kategori: data.kode_kategori } }"
            class="btn btn-warning me-3">
          Update
        </router-link>
        <button
            type="button"
            class="btn btn-danger"
            v-on:click="deleteKategori(data.kode_kategori)">
          Delete
        </button>
      </td>
    </tr>
    </tbody>

    <hr>

    <div class="modal-body">
      <input
          class="form-control"
          type="text"
          v-model="insertkode_kategori"
          placeholder="Kode Kategori"
          aria-label="default input example"/><br/>
      <input
          class="form-control"
          type="text"
          v-model="insertkategori"
          placeholder="Kategori"
          aria-label="default input example"/><br/>
      <button
          type="button"
          class="btn btn-primary"
          v-on:click="postKategori()">
        Tambah Kategori
      </button>
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

.modal-body {
  padding-left: 40pt;
  padding-right: 40pt;
}

</style>