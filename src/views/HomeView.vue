<template>
  <div class="home">
    <Header @showModal="showModal" />
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      :list="list"
      :editContact="editContact"
    />

    <div class="content">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Contatos</th>
            <th scope="col">E-mail</th>
            <th scope="col">Telefone</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in list" :key="contact.id">
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.telephone }}</td>
            <td class="actions">
              <button @click="edit(contact)" class="btn btn-action">
                <img class="icon-action" src="@/assets/ic-edit.svg" alt="Editar">
              </button>
              <button @click="remove(contact)" class="btn btn-action">
                <img class="icon-action" src="@/assets/ic-delete.svg" alt="Excluir">
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

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
      editContact: {},
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
      this.showModal();
      this.editContact = { ...item };
    },
    remove(item) {
      const idx = this.list.indexOf(item);
      this.list.splice(idx, 1);
      localStorage.setItem("contacts", JSON.stringify(this.list));
    },

    filter() {
      if (this.filters.numeroNFE != "") {
        return this.filters;
      }
    },
  },
};
</script>

<style>
body {
  background-color: #f8f9fd;
}

.table thead {
  box-shadow: inset 0 -1px 0 rgb(0 0 0 / 12%);
  height: 2.5rem;
}

.table th {
  font-size: 0.813rem;
  font-weight: 400;
  font-stretch: normal;
  font-style: normal;
  line-height: normal;
  letter-spacing: normal;
  color: #9198af;
}

.table {
  background-color: #fff;
  border: 1px solid #e1e1e1;
  border-spacing: 0px;
  width: 100%;
}

.table td.actions {
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
}

.table button.btn.btn-action {
    height: 36px;
    width: 36px;
    background: transparent;
    border: none;
}

.table button.btn.btn-action:hover {
    cursor: pointer;
    transform: scale(1.1);
    box-shadow: inset 0 0 0 1px hsla(0,0%,100%,.16),0 0 0 .5px rgba(0,0,0,.08),inset 0 0 0 .5px rgba(0,0,0,.08),0 2px 4px .5px rgba(0,0,0,.16)!important;
    background: #fff0ef;
    border-radius: 25px;
}

.table button.btn.btn-action .icon-action {
    height: 16px;
}

.table tr:hover {
    background-color: #fff3f2!important;
}
</style>