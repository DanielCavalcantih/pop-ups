<template>
  <form class="container" v-if="!openPop && openLeftPop">
    <div class="img">
      <h2 class="header">{{bodyContent.title}}</h2>
    </div>
    <div class="container-game">
      <h3>{{bodyContent.subTitle}}</h3>
      <iframe class="video" :src="bodyContent.videoUrl" title="YouTube video player" frameborder="0" allowfullscreen></iframe>
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
    </div>
    <div class="buttons">
      <button class="button" type="submit" @submit="this.continue">Continuar</button>
      <button class="button" type="button" @click="close">Fechar</button>
    </div>
  </form>
</template>

<script>
  import { mask } from 'vue-the-mask';
  import content from '@/services/videopop.json'

  export default {
    name: 'LeftPopUp',
    props: ['openLeftPop', 'openPop', 'closeLeftPop'],
    directives: {mask},
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
          genre: ''
        }
      }
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
        return json;
      },
      continue() {
        this.sendJson();
        this.closeLeftPop();
      },
      close() {
        this.closeLeftPop();
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
  }
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@100;200;300;400;500;600;700;800&display=swap');

  @keyframes slideInFromLeft {
    0% {
      transform: translateX(-100%);
    }
    100% {
      transform: translateX(0);
    }
  }

  .video {
    border-radius: 10px;
    width: 100%;
    height: 200px;
  }

  .img {
    width: 100%;
    height: 50px;
    display: flex;
    justify-content: center;
    box-shadow: none;
  }

  .container {
    position: fixed;
    left: 30px;
    bottom: 30px;
    display: flex;
    flex-direction: column;
    height: 560px;
    width: 400px;
    border-radius: 10px;
    background-size: cover;
    box-shadow: 0 0 20px black;
    animation: 0.5s ease-out 0s 1 slideInFromLeft;
    background-image: none;
    background-color: black;
  }

  .container-game {
    background-color: black;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    align-self: center;
    margin-top: 15px;
    padding: 10px;
    border-radius: 20px;
  }

  .header {
    color: white;
    font-size: 30px;
    width: 100%;
    font-weight: 400;
    text-align: center;
    line-height: 30px;
    font-family: 'Lexend', sans-serif;
    margin-top: 20px;
    padding: 0;
  }

  h3 {
    font-family: 'Lexend', sans-serif;
    font-size: 20px;
    line-height: 25px;
    font-weight: 0;
    color: white;
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
    width: 80%;
    padding: 10px 0 10px 15px;
    box-shadow: 0 0 5px black;
    border: solid 1px gray;
    border-width: 0 0 1px 0;
    color: white;
    font-size: 16px;
    margin-bottom: 10px;
    outline: none;
    background: none;
  }

  .number-genre {
    display: flex;
    width: 83%;
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
  }

  .buttons {
    width: 83%;
    display: flex;
    justify-content: space-between;
    align-self: center;
    margin-top: 10px;
  }

  .button {
    width: 40%;
    padding: 5px 20px;
    font-size: 16px;
    border-radius: 5px;
    border: none;
    box-shadow: 0 0 5px black;
    font-family: 'Lexend', sans-serif;
    cursor: pointer;
    color: white;
    background: none;
    border: solid 1px white;
  }
</style>