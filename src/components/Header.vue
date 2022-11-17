<template>
  <div class="content">
    <div class="navbar align-center justify-space-between">
      <img
        alt="Ubook - Clicksign"
        class="ubook-logo"
        src="../assets/logo-ubook.svg"
      />
      <div id="app">
        <button type="button" class="btn-create" @click="showModal">
          + Criar contato
        </button>

      </div>
      <input type="text" class="search" placeholder="Buscar..." />
    </div>
  </div>
</template>

<script>
import Modal from "@/components/Modal.vue";

export default {
  name: "Header",
  components: {
    Modal,
  },
  data() {
    return {
      isModalVisible: false,
    };
  },
  methods: {
    showModal() {
      this.$emit('showModal');
    },
  },
};
</script>

<style>
.content {
  max-width: 1440px;
  margin: 0 auto;
}

.ubook-logo {
  width: 148px;
  height: 32px;
}

.navbar {
  display: flex;
  padding: 10px;
}

.justify-space-between {
  justify-content: space-between;
}

.btn-create {
  background-color: #dbff90;
  border: 1px solid #dbff90;
  box-shadow: 2px 2px 5px 0px rgb(63 64 61 / 25%);
  min-width: 64px;
  padding: 0 16px;
  height: 40px;
  color: #fa7268;
  border-radius: 20px;
  font-weight: 500;
  font-size: 14px;
  cursor: pointer;
}

input.search {
  width: 64.5rem;
  height: 2rem;
  margin: 0 0 0 0rem;
  padding: 0.438rem 0.5rem 0.375rem;
  border-radius: 4px;
  background-color: #e4e7f4;
  border: none;
}
</style>