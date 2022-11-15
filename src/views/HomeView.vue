<template>
  <div class="home">
    <Header @showModal="showModal" />
    <Modal v-show="isModalVisible" @close="closeModal" />

    <table class="table">
      <thead>
        <tr>
          <th scope="col">id</th>
          <th scope="col">Nome</th>
          <th scope="col">E-mail</th>
          <th scope="col">Telefone</th>
          <th scope="col">Ação</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in list" :key="contact.id">
          <th scope="row">{{ contact.id }}</th>
          <td>{{ contact.name }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.telephone }}</td>
          <td>
            <button @click="edit(item)" class="btn btn-info">Editar</button>
            <button @click="remove(item)" class="btn btn-danger">
              Excluir
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Modal from "@/components/Modal.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "HomeView",
  data() {
    return {
      list: [],
      isModalVisible: false,
    };
  },
  components: {
    Header,
    Modal,
    Footer,
  },
  mounted() {
    const contacts = JSON.parse(localStorage.getItem("contacts"));
    this.list = contacts ? contacts : [];
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    
    edit(item) {
      this.index = this.list.indexOf(item);
      this.contact = Object.assign({}, item);
      localStorage.setItem("contacts", JSON.stringify(this.list));
    },
  },
};
</script>

<style scoped>
th {
  color: #000;
}
</style>