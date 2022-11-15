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
          <slot name="header"> Novo contato </slot>
          <button
            type="button"
            class="btn-close"
            @click="close"
            aria-label="Close modal"
          >
            x
          </button>
        </header>

        <section class="modal-body" id="modalContent">
          <slot name="body">
            <label for="name">Nome:</label>
            <input type="text" name="name" />

            <label for="email">E-mail:</label>
            <input type="email" name="email" />

            <label for="phone">Telefone:</label>
            <input type="tel" name="phone" placeholder="(xx) xxxxx-xxxx" />
          </slot>
        </section>

        <footer class="modal-footer">
          <button
            type="button"
            class="btn btn-transparent"
            @click="close"
            aria-label="Close modal"
          >
            Cancelar
          </button>
          <button
            type="button"
            class="btn btn-coral"
            @click="saveContact()"
            aria-label="Close modal"
          >
            Salvar
          </button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Modal",
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>


<style>
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
  width: 430px;
  position: relative;
  padding: 5px 15px 20px;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #fa7268;
  justify-content: space-between;
  font-weight: bold;
  font-size: 15px;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}

.btn-close {
  position: absolute;
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
  border-radius: 2px;
  font-weight: bold;
  height: 30px;
  border-radius: 20px;
}

.btn-coral {
  color: white;
  background: #fa7268;
  border: 1px solid #fff;
  width: 80px;
  height: 30px;
  border-radius: 20px;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s ease;
}

label {
  text-align: left;
  padding: 10px 0px 5px;
  font-weight: bold;
  font-size: 14px;
}

input {
  line-height: 20px;
  padding: 8px 0;
  max-width: 100%;
  min-width: 0;
  width: 100%;
}
</style>