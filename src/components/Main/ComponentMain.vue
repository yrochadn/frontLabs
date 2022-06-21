<template>
  <div>
    <main>
      <button class="btnAdd" @click="showMeCode">Adicionar</button>

      <table class="table table-striped">
        <thead>
          <tr>
            <th>Nome do Produto</th>
            <th>Descrição do Produto</th>
            <th>Fornecedor</th>
            <th>Quantidade</th>
            <th>Opções</th>
          </tr>
        </thead>

        <tbody v-for="product in products" :key="product.id">
          <!-- primeira linha -->
          <tr>
            <td>{{ product.nome }}</td>
            <td>{{ product.descricao }}</td>
            <td>{{ product.fornecedor }}</td>
            <td>{{ product.quantidade }}</td>
            <td>
              <svg
                @click="showMeCodeEdit"
                class="icon"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 512 512"
              >
                <!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M362.7 19.32C387.7-5.678 428.3-5.678 453.3 19.32L492.7 58.75C517.7 83.74 517.7 124.3 492.7 149.3L444.3 197.7L314.3 67.72L362.7 19.32zM421.7 220.3L188.5 453.4C178.1 463.8 165.2 471.5 151.1 475.6L30.77 511C22.35 513.5 13.24 511.2 7.03 504.1C.8198 498.8-1.502 489.7 .976 481.2L36.37 360.9C40.53 346.8 48.16 333.9 58.57 323.5L291.7 90.34L421.7 220.3z"
                />
              </svg>

              <!-- <button type="button" class="btn" @click="showMeCodeEdit">
                Editar
              </button> -->

              <svg
                @click="showMeCodeDelete"
                class="icon"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 448 512"
              >
                <!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M135.2 17.69C140.6 6.848 151.7 0 163.8 0H284.2C296.3 0 307.4 6.848 312.8 17.69L320 32H416C433.7 32 448 46.33 448 64C448 81.67 433.7 96 416 96H32C14.33 96 0 81.67 0 64C0 46.33 14.33 32 32 32H128L135.2 17.69zM394.8 466.1C393.2 492.3 372.3 512 346.9 512H101.1C75.75 512 54.77 492.3 53.19 466.1L31.1 128H416L394.8 466.1z"
                />
              </svg>

              <!-- <button type="button" class="btnEx" @click="showMeCodeDelete">
                Excluir
              </button> -->
            </td>
          </tr>
        </tbody>
      </table>
    </main>
  </div>

  <!-- MODAL BOTÃO ADICIONAR -->
  <div class="modal-main" v-show="showMe">
    <div class="modalAdd">
      <form>
        <label>Nome do Produto</label>
        <input type="text" />

        <label>Descrição do Produto</label>
        <input type="text" />

        <label>Fornecedor</label>
        <input type="text" />

        <label>Quantidade</label>
        <input type="text" />
      </form>
      <span class="close" @click="unShowMeCode">
        <p>X</p>
      </span>

      <button class="btnForm" @click="alertMessageAdd">Adicionar</button>
    </div>
  </div>

  <!-- MODAL BOTÃO EDITAR -->
  <div class="modal-main" v-show="showMeEdit">
    <div class="modalAdd">
      <form>
        <label>Nome do Produto</label>
        <input type="text" />

        <label>Descrição do Produto</label>
        <input type="text" />

        <label>Fornecedor</label>
        <input type="text" />

        <label>Quantidade</label>
        <input type="text" />
      </form>
      <span class="close" @click="unShowMeCodeEdit">
        <p>X</p>
      </span>
      <button class="btnForm" @click="alertMessageEdit">Editar</button>
    </div>
  </div>

  <!-- MODAL BOTÃO EXCLUIR -->
  <div class="modal-main" v-show="showMeDelete">
    <div class="modalAdd">
      <svg
        class="iconAlert"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 512 512"
      >
        <path
          d="M506.3 417l-213.3-364c-16.33-28-57.54-28-73.98 0l-213.2 364C-10.59 444.9 9.849 480 42.74 480h426.6C502.1 480 522.6 445 506.3 417zM232 168c0-13.25 10.75-24 24-24S280 154.8 280 168v128c0 13.25-10.75 24-23.1 24S232 309.3 232 296V168zM256 416c-17.36 0-31.44-14.08-31.44-31.44c0-17.36 14.07-31.44 31.44-31.44s31.44 14.08 31.44 31.44C287.4 401.9 273.4 416 256 416z"
        />
      </svg>

      <h2>Deseja Excluir este item?</h2>
      <span class="close" @click="unShowMeCodeDelete">
        <p>X</p>
      </span>
      <button class="btnForm" @click="alertMessageRemove">Excluir</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showMe: false,
      showMeEdit: false,
      showMeDelete: false,

      products: [
        {
          id: 1,
          nome: "Maçã",
          descricao: "Vermelha",
          fornecedor: "TutiFruit",
          quantidade: "5",
        },
        {
          id: 2,
          nome: "Pera",
          descricao: "Verde",
          fornecedor: "TutiFruit",
          quantidade: "4",
        },
        {
          id: 3,
          nome: "Melancia",
          descricao: "Vermelha",
          fornecedor: "TutiFruit",
          quantidade: "10",
        },
        {
          id: 4,
          nome: "Uva",
          descricao: "Roxa",
          fornecedor: "TutiFruit",
          quantidade: "100",
        },
        {
          id: 5,
          nome: "Mamão",
          descricao: "Amarelo",
          fornecedor: "TutiFruit",
          quantidade: "20",
        },
        // {
        //   id: 6,
        //   nome: "Melão",
        //   descricao: "Verde",
        //   fornecedor: "TutiFruit",
        //   quantidade: "20",
        // },
        // {
        //   id: 7,
        //   nome: "Morango",
        //   descricao: "Vermelho",
        //   fornecedor: "TutiFruit",
        //   quantidade: "50",
        // },
        // {
        //   id: 8,
        //   nome: "Jaca",
        //   descricao: "Verde",
        //   fornecedor: "TutiFruit",
        //   quantidade: "40",
        // },
        // {
        //   id: 9,
        //   nome: "Maçã",
        //   descricao: "Verde",
        //   fornecedor: "TutiFruit",
        //   quantidade: "80",
        // },
        // {
        //   id: 10,
        //   nome: "Kiwi",
        //   descricao: "Azedo",
        //   fornecedor: "TutiFruit",
        //   quantidade: "50",
        // },
      ],
    };
  },

  methods: {
    showMeCode() {
      this.showMe = true;
    },

    unShowMeCode() {
      this.showMe = false;
    },

    showMeCodeEdit() {
      this.showMeEdit = true;
    },

    unShowMeCodeEdit() {
      this.showMeEdit = false;
    },

    showMeCodeDelete() {
      this.showMeDelete = true;
    },

    unShowMeCodeDelete() {
      this.showMeDelete = false;
    },

    alertMessageAdd() {
      alert("Adicionado com sucesso!");
    },

    alertMessageEdit() {
      alert("Editado com sucesso!");
    },

    alertMessageRemove() {
      alert("Excluido com sucesso!");
    },
  },
};
</script>

<style scoped>
.btnAdd {
  width: 100px;
  height: 25px;
  background-color: #243b4a;
  border: 1px solid #eee;
  border-radius: 10px;
  cursor: pointer;
  margin-top: 0.5rem;
  margin-left: 0.5rem;
  color: #eee;
  font-size: 16px;
}

.btnAdd:active {
  box-shadow: 2px, #c4c4c4;
  transform: translateY(4px);
}
.table,
.table-striped {
  width: 100%;
  height: auto;
  margin-top: 1rem;
  background-color: #e4e4e4;
  line-height: 2rem;
}

.table,
.table-striped,
thead tbody {
  text-align: center;
  padding: 10px;
}

.table,
.table-striped,
tbody button {
  padding: 5px;
}

.btn {
  background-color: #3fa7d6;
  border-radius: 10px;
  width: 50px;
  color: #eee;
  height: 30px;
  margin-left: 0.5rem;
  cursor: pointer;
  font-size: 12px;
  border: none;
}

.btn:active {
  background-color: #3fa7d6;
  transform: translateY(4px);
}

.btnEx {
  background-color: #ee6352;
  border-radius: 10px;
  width: 50px;
  color: #eee;
  height: 30px;
  margin-left: 0.5rem;
  cursor: pointer;
  font-size: 12px;
  border: none;
}

.btnEx:active {
  background-color: #ee6352;
  transform: translateY(4px);
}

.modal-main {
  position: absolute;
  width: 100%;
  height: 100vh;
  background-color: #eee;
  top: 0;
  opacity: 0.95;
}
.modalAdd {
  background-color: #220195;
  padding: 40px;
  margin-top: 10rem;
  margin-left: 20rem;
  margin-right: 20rem;
}

.modalAdd h2 {
  text-align: center;
  color: #fff;
}
.modalAdd .btnForm {
  margin-left: 90%;
  width: 80px;
  height: 40px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

.modalAdd .btnForm:hover {
  background-color: #36827f;
  color: #fff;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

form {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

form label {
  font-size: 15px;
  font-family: monospace;
  font-weight: 400;
  margin-bottom: 0.5rem;
  margin-top: 1rem;
  color: #fff;
}

form input {
  width: 36%;
  padding: 5px;
  border-radius: 8px;
  border-style: none;
}

.close {
  position: absolute;
  width: 35px;
  height: 35px;
  top: 21%;
  left: 78%;
  font-weight: bold;
  background-color: red;
  border-radius: 50%;
  font-size: 25px;
  color: white;
  cursor: pointer;
}

.close p {
  margin-left: 25%;
  margin-top: 5%;
}

.icon {
  width: 15px;
  font-size: 10px;
  cursor: pointer;
  margin-left: 1rem;
  margin-right: 1rem;
}
.iconAlert{
  width: 150px;
  font-size: 10px;
  margin-left: 21rem;
  opacity: 1;
  margin-bottom: 2rem;

}
</style>