<template>
  <div className="container">
    <h1 className="mt-4 text-center">Students</h1>
    <form>
      <div className="form-group">
        <label for="broj_indexa">Broj Indexa: </label>
        <input
          type="number"
          placeholder="Broj Indexa"
          v-model="broj_indexa"
          className="form-control"
        />
      </div>
      <div className="form-group">
        <label for="ime">Ime: </label>
        <input
          type="text"
          placeholder="Ime"
          v-model="ime"
          className="form-control"
        />
      </div>
      <div className="form-group">
        <label for="prezime">Prezime: </label>
        <input
          type="text"
          placeholder="Prezime"
          v-model="prezime"
          className="form-control"
        />
      </div>
      <div className="form-group">
        <label for="godina">Godina: </label>
        <input
          type="number"
          placeholder="Godina"
          v-model="godina"
          className="form-control"
        />
      </div>
      <div className="form-group">
        <label for="status-studenta">Status Studenta: </label>
        <input
          type="text"
          placeholder="Status Studenta"
          v-model="status_studenta"
          className="form-control"
        />
      </div>
      <button type="button" @click="onSubmit" className="btn btn-dark">
        Submit
      </button>
    </form>
     <table className="table mt-5">
      <thead>
        <tr>
          <th scope="col">PK Student ID</th>
          <th scope="col">Broj Indexa</th>
          <th scope="col">Ime</th>
          <th scope="col">Prezime</th>
          <th scope="col">Godina</th>
          <th scope="col">Status Studenta</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(entry, i) in sortedList" :key="i">
          <th scope="row">{{ ++i }}</th>
          <td>{{ entry.broj_indexa }}</td>
          <td>{{ entry.ime }}</td>
          <td>{{ entry.prezime }}</td>
          <td>{{ entry.godina }}</td>
          <td>{{ entry.status_studenta }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template> 

<script>
export default {
  name: "WelcomeItem",
  data: () => ({ broj_indexa: "", ime: "", prezime: "", godina: "", status_studenta: "", allStudents: [] }),
  computed: {
    sortedList: function() {
      return this.allStudents.slice().sort(function(a, b) {
        return b.prezime - a.prezime;
      });
    },
  },
    mounted() {
    if (localStorage.getItem('allStudents')) {
      try {
        this.allStudents = JSON.parse(localStorage.getItem('allStudents'));
      } catch(e) {
        localStorage.removeItem('allStudents');
      }
    }
  },
  methods: {
    onSubmit() {
      this.allStudents.push({ broj_indexa: this.broj_indexa, ime: this.ime, prezime: this.prezime, godina: this.godina, status_studenta: this.status_studenta,});
      this.clearForm();
      this.saveAllStudents();
    },
    clearForm() {
      this.broj_indexa = "";
      this.ime = "";
      this.prezime = "";
      this.godina = ""; 
      this.status_studenta = "";
    },
        saveAllStudents() {
      const parsed = JSON.stringify(this.allStudents);
      localStorage.setItem('allStudents', parsed);
    }
  },
};
</script>