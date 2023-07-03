<script>
import axios from 'axios';
import { ref } from 'vue';

const readAllBuku = 'http://localhost/pustaka-buku/readallbuku.php';
const insertBuku = 'http://localhost/pustaka-buku/insertbuku.php';
const delBuku = 'http://localhost/pustaka-buku/deletebuku.php';

export default {
  data() {
    return {
      buku: ref([]),
      insertkode_buku: '',
      insertkode_kategori: '',
      insertjudul: '',
      insertpengarang: '',
      insertpenerbit: '',
      inserttahun: '',
      insertharga: '',
    };
  },
  mounted() {
    this.readBuku();
  },
  methods: {
    readBuku() {
      axios
          .get(readAllBuku)
          .then((resp) => {
            console.log(resp);
            this.buku = resp.data;
          })
          .catch((err) => {
            console.log(err);
          });
    },

    postBuku() {
      let formData = new FormData();

      formData.append('kode_buku', this.insertkode_buku);
      formData.append('kode_kategori', this.insertkode_kategori);
      formData.append('judul', this.insertjudul);
      formData.append('pengarang', this.insertpengarang);
      formData.append('penerbit', this.insertpenerbit);
      formData.append('tahun', this.inserttahun);
      formData.append('harga', this.insertharga);

      axios
          .post(insertBuku, formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
            },
          })
          .then((resp) => {
            console.log(resp.data);
            this.readBuku();
            this.insertkode_buku = '';
            this.insertkode_kategori = '';
            this.insertjudul = '';
            this.insertpengarang = '';
            this.insertpenerbit = '';
            this.inserttahun = '';
            this.insertharga = '';
          })
          .catch((err) => {
            console.log(err);
          });
    },

    deleteBuku(kode_buku) {
      if (confirm('Apakah Anda yakin ingin mendelete data buku?')) {
        axios
            .get(delBuku + '?kode_buku=' + kode_buku)
            .then((resp) => {
              console.log(resp);
              this.readBuku();
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
      <div class="welcome">Daftar Buku Perpustakaan Digital</div>
    </div>

    <thead>
    <tr>
      <td class="border" style="text-align: center;width: 175px"><strong>Kode Buku</strong></td>
      <td class="border" style="text-align: center;width: 150px"><strong>Kode Kategori</strong></td>
      <td class="border" style="text-align: center;width: 500px"><strong>Judul</strong></td>
      <td class="border" style="text-align: center;width: 400px"><strong>Pengarang</strong></td>
      <td class="border" style="text-align: center;width: 400px"><strong>Penerbit</strong></td>
      <td class="border" style="text-align: center;width: 100px"><strong>Tahun</strong></td>
      <td class="border" style="text-align: center;width: 150px"><strong>Harga</strong></td>
      <td class="border" style="text-align: center;width: 315px"><strong>Aksi</strong></td>
    </tr>
    </thead>
    <tbody>
    <tr v-for="data in buku">
      <td>{{ data.kode_buku }}</td>
      <td>{{ data.kode_kategori }}</td>
      <td>{{ data.judul }}</td>
      <td>{{ data.pengarang }}</td>
      <td>{{ data.penerbit }}</td>
      <td>{{ data.tahun }}</td>
      <td>Rp. {{ data.harga }}</td>
      <td>
        <router-link
            :to="{ name: 'updatebuku', params: { kode_buku: data.kode_buku } }"
            class="btn btn-warning me-3">
          Update
        </router-link>
        <button
            type="button"
            class="btn btn-danger"
            v-on:click="deleteBuku(data.kode_buku)">
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
          v-model="insertkode_buku"
          placeholder="Kode Buku"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="insertkode_kategori"
          placeholder="Kode Kategori"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="insertjudul"
          placeholder="Judul"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="insertpengarang"
          placeholder="Pengarang"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="insertpenerbit"
          placeholder="Penerbit"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="text"
          v-model="inserttahun"
          placeholder="Tahun"
          aria-label="default input example" /><br />
      <input
          class="form-control"
          type="number"
          v-model="insertharga"
          placeholder="Harga"
          aria-label="default input example" /><br />
      <button
          type="button"
          class="btn btn-primary"
          v-on:click="postBuku()">
        Tambah Buku
      </button>
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
  padding-bottom: 10pt;
}

</style>