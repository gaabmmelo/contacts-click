<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalContent"
      >
        <header class="modal-header" id="modalTitle">
          <slot name="header">
            <p class="title-modal">Excluir contato</p>
          </slot>
          <button
            type="button"
            class="btn-close"
            @click="closeModal"
            aria-label="Close modal"
          >
            x
          </button>
        </header>

        <section class="modal-body" id="modalContent">
          <slot name="body">
            <p>Deseja realmente excluir o contato?</p>
          </slot>
        </section>

        <footer class="modal-footer">
          <button
            type="button"
            class="btn btn-transparent"
            @click="closeModal()"
          >
            Cancelar
          </button>
          <button type="button" class="btn btn-coral" @click="remove(contact)">
            Excluir
          </button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ModalDelete",
  props: ["list", "deleteContact"],
  watch: {
    deleteContact: function (deleteVal) {
      this.contact = deleteVal;
    },
  },
  methods: {
    remove(item) {
      const idx = this.list.indexOf(item);
      this.list.splice(idx, 1);
      localStorage.setItem("contacts", JSON.stringify(this.list));
      this.$emit("close");
    },
    closeModal() {
      this.$emit("close");
      this.contact = { id: 0, name: null, email: null, telephone: null };
    },
  },
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal #modalContent {
  display: flex;
  flex-direction: column;
  position: relative;
  padding: 5px 1.5rem 1.375rem;
}

.modal {
  background: #ffffff;
  box-shadow: 0 16px 10px 0 rgb(0 0 0 / 8%);
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  border-radius: 16px;
  width: 27rem;
  height: 12.938rem;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #c0c3d2;
  justify-content: space-between;
  font-size: 1rem;
  color: #2a2d3b;
  font-weight: normal;
  display: flex;
}

.modal-header p {
  margin: 1rem 7.75rem 0.781rem 1rem;
}

.modal-body p {
  color: #2a2d3b;
  text-align: left;
  margin-top: 1.219rem;
  font-family: roboto, sans-serif;
  font-size: 0.875rem;
  font-weight: normal;
}

.modal-footer {
  border-top: 1px solid #c0c3d2;
  padding: 0.938rem 1rem 1rem;
  flex-direction: column;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}

.btn-close {
  position: absolute;
  cursor: pointer;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  font-weight: bold;
  color: #fa7268;
  background: transparent;
}

.btn {
  cursor: pointer;
}

.btn-transparent {
  color: #fa7268;
  background: transparent;
  border: 1px solid #fff;
  font-weight: bold;
  border-radius: 16px;
  margin: 0px 0.5rem;
  padding: 0.5rem 1rem;
  width: 5.5rem;
  height: 2rem;
}

.btn-transparent:hover {
  background-color: #fa726824 !important;
}

.btn-coral {
  color: white;
  background: #fa7268;
  border: 1px solid #fff;
  width: 4.5rem;
  height: 2rem;
  border-radius: 16px;
  font-family: roboto, sans-serif;
  font-size: 0.875rem;
  font-weight: 500;
  line-height: normal;
}

.btn-coral:disabled {
  opacity: 0.32;
}

.btn-coral:hover {
  background-color: #e85a50;
  transition: 0.7s;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.2s ease;
}
</style>
