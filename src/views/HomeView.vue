<template>
  <div class="home">
    <Header @showModal="showModal" @filterContacts="filterContacts" />
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      :list="list"
      :editContact="editContact"
    />

    <ModalDelete
      v-show="isModalVisibleDelete"
      @close="closeModalDelete"
      :list="list"
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
          <!--contact in list-->
          <tr v-for="contact in this.filteredContacts" :key="contact.id">
            <td><button class="alpha-order">{{ contact.name.charAt(0).toUpperCase() }}</button> {{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.telephone }}</td>
            <td class="actions">
              <button @click="edit(contact)" class="btn btn-action">
                <img
                  class="icon-action"
                  src="@/assets/ic-edit.svg"
                  alt="Editar"
                />
              </button>
              <button @click="showModalDelete" class="btn btn-action">
                <img
                  class="icon-action"
                  src="@/assets/ic-delete.svg"
                  alt="Excluir"
                />
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
import Header from "@/components/Header.vue";
import Modal from "@/components/Modal.vue";
import ModalDelete from "@/components/ModalDelete.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "HomeView",
  data() {
    return {
      list: [],
      filteredContacts: [],
      isModalVisible: false,
      isModalVisibleDelete: false,
      editContact: {},
    };
  },
  components: {
    Header,
    Modal,
    ModalDelete,
    Footer,
  },
  mounted() {
    const contacts = JSON.parse(localStorage.getItem("contacts"));
    this.list = contacts ? contacts : [];
    this.filterContacts();
  },
  methods: {
    filterContacts(search = null) {
      console.log(search);
      this.filteredContacts = this.list;
      if (search) {
        this.filteredContacts = this.list.filter((contact) => {
          return (
            contact.name.toLowerCase().includes(search.toLowerCase()) ||
            contact.email.toLowerCase().includes(search.toLowerCase()) ||
            contact.telephone.toLowerCase().includes(search.toLowerCase())
          );
        });
      }
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    showModalDelete() {
      this.isModalVisibleDelete = true;
    },
    closeModalDelete() {
      this.isModalVisibleDelete = false;
    },
    edit(item) {
      this.showModal();
      this.editContact = { ...item };
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
  box-shadow: inset 0 0 0 1px hsla(0, 0%, 100%, 0.16),
    0 0 0 0.5px rgba(0, 0, 0, 0.08), inset 0 0 0 0.5px rgba(0, 0, 0, 0.08),
    0 2px 4px 0.5px rgba(0, 0, 0, 0.16) !important;
  background: #fff0ef;
  border-radius: 25px;
}

.table button.btn.btn-action .icon-action {
  height: 16px;
}

.table tbody tr:hover {
  background-color: #fff3f2 !important;
}

.table .alpha-order {
    height: 24px;
    width: 24px;
    background-color: #fa8d68;
    border: unset;
    border-radius: 20px;
    color: white;
    font-weight: bold;
}

</style>