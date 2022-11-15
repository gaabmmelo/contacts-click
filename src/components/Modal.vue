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
            <input type="text" name="name" v-model="contact.name" />

            <label for="email">E-mail:</label>
            <input type="email" name="email" v-model="contact.email" />

            <label for="telephone">Telefone:</label>
            <input
              type="tel"
              name="telephone"
              placeholder="(xx) xxxxx-xxxx"
              v-model="contact.telephone"
            />
          </slot>
        </section>

        <footer class="modal-footer">
          <button
            type="button"
            class="btn btn-transparent"
            @click="close()"
          >
            Cancelar
          </button>
          <button
            type="button"
            class="btn btn-coral"
            @click="add()"
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
  data() {
    return {
      contact: {
        id: 0,
        name: null,
        email: null,
        telephone: null,
      },
      index: null,
      list: [],
    };
  },
  methods: {
    add() {
      if (this.contact.id === 0) {
        this.contact.id = this.list.length + 1;
        this.list.push(this.contact);
      } else {
        this.list[this.index] = this.contact;
      }
      localStorage.setItem("contacts", JSON.stringify(this.list));
      this.contact = { id: 0, name: null, email: null, telephone: null };
    },

    remove(item) {
      const idx = this.list.indexOf(item);
      this.list.splice(idx, 1);
      localStorage.setItem("contacts", JSON.stringify(this.list));
    },

    edit(item) {
      this.index = this.list.indexOf(item);
      this.contact = Object.assign({}, item);
      localStorage.setItem("contacts", JSON.stringify(this.list));
    },
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
  box-shadow: 0 16px 10px 0 rgb(0 0 0 / 8%);
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
  transition: opacity 0.5s ease;
}

label {
  text-align: left;
  padding: 10px 0px 5px;
  font-size: 14px;
  font-weight: normal;
}

.modal input {
  line-height: 20px;
  padding: 0px 0;
  height: 30px;
  font-size: 15px;
  padding: 0px 5px;
  border-radius: 10px;
  border: 1px solid #00000070;
}
</style>