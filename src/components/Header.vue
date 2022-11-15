<template>
  <div class="content">
    <div class="navbar align-center justify-space-between">
      <img
        alt="Ubook - Clicksign"
        class="ubook-logo"
        src="../assets/logo-ubook.png"
      />
      <button type="button" class="btn-create" @click="openModalContact()">+ Criar contato</button>
      <input type="text" class="search" placeholder="Pesquisar...">
    </div>
  </div>
</template>

<script>
import Modal from '@/components/Modal.vue';

export default {
  components: {
     Modal,
  },
  data: {

  },
  methods: {
    openModalContact() {
      
    }
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
}

input.search {
    width: 70%;
    background-color: #e4e7f4;
    border: 1px solid #e4e7f4;
    border-radius: 4px!important;
    font-size: 14px;
    color: #9198af;
    padding-left: 10px;
}
</style>