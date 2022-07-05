//Profession//
<template>
  <h2>Profession</h2>
  <div>
    <form @submit.prevent="add">
      <input type="hidden" v-model="form.id" />
      <input type="text" v-model="form.name" />
      <input type="date" v-model="form.created_at" />
      <input type="date" v-model="form.updated_at" />
      <button type="submit" v-show="!updateSubmit">Add</button>
      <button type="button" v-show="updateSubmit" @click="update(form)">Update</button>
    </form>
    <ul v-for="profession in profession" :key="profession.idd">
      <li>
        <span>{{ profession.name }}</span> &#160; <button @click="edit(profession)">Edit</button> || <button @click="del(profession)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
export default {
  data() {
    return {
      form: {
        id: "",
        name: "",
        created_at: "",
        updated_at: "",
      },
      professions: "",
      updateSubmit: false,
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      axios
        .get("https://test-case.fe.can.co.id/api/profession")
        .then((res) => {
          this.professions = res.data;
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    add() {
      axios.post("https://test-case.fe.can.co.id/api/profession", this.form).then((res) => {
        this.load();
        this.form.name = "";
        this.form.created_at = "";
        this.form.updated_at = "";
      });
    },
    edit(profession) {
      this.updateSubmit = true;
      this.form.id = profession.id;
      this.form.name = profession.name;
      this.form.created_at = profession.created_at;
      this.form.updated_at = profession.updated_at;
    },
    update(form) {
      return axios
        .put("https://test-case.fe.can.co.id/api/profession/134" + form.id, { name: this.form.name })
        .then((res) => {
          this.load();
          this.form.id = "";
          this.form.name = "";
          this.form.created_at = "";
          this.form.updated_at = "";
          this.updateSubmit = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    del(profession) {
      axios.delete("https://test-case.fe.can.co.id/api/profession/1" + profession.id).then((res) => {
        this.load();
        let index = this.professions.indexOf(form.name);
        this.professions.splice(index, 1);
      });
    },
    show() {
      axios
        .get("https://test-case.fe.can.co.id/api/profession/2")
        .then((res) => {
          this.professions = res.data.data;
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
