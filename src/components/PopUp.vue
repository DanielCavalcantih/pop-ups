<template>
  <div class="modal" v-if="openPop">
    <form class="container">
      <div class="img">
        <h2 class="header">{{bodyContent.title}}</h2>
        <img width="120" src="https://i.pinimg.com/originals/e6/f0/c4/e6f0c41e35778209247cc6f1bc7a3e5b.png" />
      </div>
      <div class="container-game">
        <h3>{{bodyContent.subTitle}}</h3>
        <img width="190" class="game" src="https://images.emojiterra.com/google/android-12l/512px/1f3b0.png" />
      </div>
      <div class="container-inputs">
        <input required v-if="bodyContent.nameField" class="input" v-model="userInfo.name" placeholder="Nome" />
        <input required v-if="bodyContent.emailField" class="input" v-model="userInfo.email" type="email" placeholder="E-mail" />
        <div :class="bodyContent.cellphoneField && bodyContent.genreField ? 'number-genre' : 'number-genre2'">
          <input required v-if="bodyContent.cellphoneField" class="input input-number" v-model="userInfo.number" v-mask="'(##) #####-####'" placeholder="Celular" />
          <select required v-if="bodyContent.genreField" class="input input-select" id="genre" v-model="userInfo.genre" placeholder="Sexo">
            <option value="" disabled selected hidden>Gênero</option>
            <option class="options" value="Masculino">Masculino</option>
            <option class="options" value="Feminino">Feminino</option>
          </select>
        </div>
        <label for="privacity" v-if="bodyContent.checkbox">
          <input type="checkbox" id="Privacity" class="check" v-model="userInfo.shareInfo" />
          Permitir compartilhar essas informações
        </label>
      </div>
      <div class="buttons">
        <button class="button continue" type="button" @click="this.continue">Continuar</button>
        <button class="button close" @click="close">Fechar</button>
      </div>
    </form>
  </div>
</template>

<script scoped>
  import { mask } from 'vue-the-mask';
  import content from '@/services/content.json'

  export default {
    name: 'PopUp',
    directives: {mask},
    props: ['openPop', 'closePopUp', 'openLeftPopUp'],
    data() {
      return {
        bodyContent: {
          title: '',
          subTitle: '',
          nameField: false,
          emailField: false,
          cellphoneField: false,
          genreField: false,
          videoUrl: '',
          checkbox: false
        },
        userInfo: {
          email: '',
          name: '',
          number: '',
          genre: '',
          shareInfo: false
        }
      }
    },
    mounted() {
      this.bodyContent.title = content.title;
      this.bodyContent.subTitle = content.subTitle;
      this.bodyContent.nameField = content.nameField;
      this.bodyContent.emailField = content.emailField;
      this.bodyContent.cellphoneField = content.cellphoneField;
      this.bodyContent.genreField = content.genreField;
      this.bodyContent.videoUrl = content.videoUrl;
      this.bodyContent.checkbox = content.checkbox;
    },
    methods: {
      sendJson() {
        const obj = {
          name: this.userInfo.name,
          email: this.userInfo.email,
          number: this.userInfo.number,
          genre: this.userInfo.genre
        }
        const json = JSON.stringify(obj);
        console.log(json);
      },
      continue() {
        this.sendJson();
        this.closePopUp();
        this.openLeftPopUp();
      },
      close() {
        this.closePopUp();
        this.openLeftPopUp();
      }
    }
  }
</script>

<style>
  @font-face {
    font-family: SaoJoao;
    src: url('../fonts/BRAZIE.ttf');
  }

  @keyframes slideInFromLeft {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(0);
    }
  }

  .modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0, 0, 0, 0.6);
    z-index: 5;
    cursor: default;
  }

  .img {
    width: 100%;
    height: 90px;
    display: flex;
    justify-content: space-between;
    align-items: start;
  }

  .container {
    display: flex;
    flex-direction: column;
    height: 600px;
    width: 500px;
    border-radius: 10px;
    background-image: url("https://www.koord.com.br/wp-content/uploads/2023/01/Geraldo_3C_2_flor-2-scaled.jpg");
    background-size: cover;
    box-shadow: 0 0 20px black;
    animation: 0.5s ease-out 0s 1 slideInFromLeft;
  }

  .container-game {
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    box-shadow: 0 0 20px;
    align-self: center;
    padding: 10px;
    border-radius: 20px;
  }

  .header {
    color: yellow;
    text-shadow: 0 3px 4px black;
    font-size: 28px;
    max-width: 72%;
    text-align: left;
    line-height: 30px;
    font-family: SaoJoao;
    padding-left: 20px;
    margin-top: 10px;
  }

  label {
    font-size: 18px;
    font-weight: 600;
    display: flex;
    align-items: center;
    cursor: pointer;
  }

  .check {
    height: 18px;
    width: 18px;
    cursor: pointer;
    margin-right: 10px;
  }

  h3 {
    font-family: SaoJoao;
    font-size: 25px;
    line-height: 25px;
    font-weight: 0;
    color: rgb(50, 50, 50);
    margin-top: 0;
    margin-bottom: 10px;
  }

  .container-inputs {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  .input {
    width: 70%;
    padding: 10px 0 10px 15px;
    border-radius: 5px;
    box-shadow: 0 0 5px black;
    border: none;
    font-size: 16px;
    margin-bottom: 10px;
    outline: none;
  }

  .number-genre {
    display: flex;
    width: 73%;
    justify-content: space-between;
  }

  .number-genre2 {
    display: flex;
    width: 73%;
    justify-content: center;
  }

  .input-number {
    width: 44%;
  }

  .input-select {
    width: 48%;
    cursor: pointer;
    background-color: white;
  }

  .buttons {
    width: 70%;
    display: flex;
    justify-content: space-between;
    align-self: center;
    margin-top: 20px;
  }

  .button {
    width: 40%;
    padding: 5px 20px;
    font-size: 16px;
    border-radius: 5px;
    border: none;
    box-shadow: 0 0 5px black;
    cursor: pointer;
  }

  .continue {
    background-color: green;
    color: white;
    font-family: SaoJoao;
    transition: 100ms;
  }

  .continue:hover {
    transform: scale(1.02);
  }

  @media screen and (max-width: 355px) {
    .container {
      transform: scale(0.6);
    }
  }

  @media screen and (max-width: 440px) {
    .header {
      font-size: 20px;
    }
  }

  @media screen and (max-width: 520px) {
    .container {
      transform: scale(0.8);
    }
  }

  @media screen and (max-height: 620px) {
    .container {
      transform: scale(0.8);
    }
  }
</style>
