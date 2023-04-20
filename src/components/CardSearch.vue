<template>
  <div class="card">
      <div class="container">
          <div class="container__title">
              <img class="github" src="../assets/github.svg" />
              <p class="title">GITHUB SEARCH</p>
          </div>
          <div class="input__area">
              <input class="input is-large is-link" type="text" placeholder="Nome do Github" v-model="github">
              <button class="button " @click="fetchUser">Pesquisar perfil</button>
          </div>
          <div class="area__user">
              <div class="area_info" v-if="login">
                  <div class="img__location">
                      <img :src="avatarUrl" alt="Avatar" class="avatar">
                  </div>
                  <div class="info__location">
                      <p class="infos title_login">{{ login }}</p>
                      <p class="infos repo">Numero de Repositorios: {{ public_repos }}</p>
                      <p class="infos">Seguidores: {{ followers }}</p>
                      <p class="infos">Seguindo: {{ following }}</p>
                      <a :href="html_url" class="infos link">Ver perfil</a>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script lang="ts">
import api from '@/http/axios';
import { GithubUser } from '@/interfaces/User';
import { AxiosResponse } from 'axios';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'CardSearch',
  data() {
      return {
          github: '',
          avatarUrl: '',
          login: '',
          public_repos: '',
          html_url: '',
          followers: 0,
          following: 0
      }
  },
  methods: {
      async fetchUser(): Promise<void> {
          try {
              const response: AxiosResponse<GithubUser> = await api.get(`/users/${this.github}`);
              this.avatarUrl = response.data.avatar_url;
              this.login = response.data.login;
              this.public_repos = response.data.public_repos;
              this.html_url = response.data.html_url;
              this.followers = response.data.followers;
              this.following = response.data.following;
          } catch (error) {
              console.log(error);
          }
      },
  }
})
</script>


<style scoped>
.card {
  background-color: #171E99;
  height: 45rem;
  width: 500px;
  border-radius: 15px;
}

.container {
  height: 100%;
  width: 80%;
}

.area_info {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.container__title {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  flex-direction: column;
  height: 30%;
}

.github {
  width: 90px;
}


.title {
  color: white;
  font-weight: 600;
  font-size: 35px;
  margin: 10px;
}

.input__area {
  height: 20%;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

}

.input {
  background-color: #011E55;
  border-radius: 10px;
  margin-top: 10px;
  color: white;
}

.input::placeholder {
  font-size: 18px;
  color: grey;
}

.button {
  width: 100%;
  background-color: #0368FF;
  border: none;
  color: white;
  height: 50px;
  font-weight: 500;

}

.area__user {
  margin-top: 20px;
  height: 45%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.img__location {
  height: 60%;
  width: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.info__location {
  width: 70%;
  height: 60%;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  flex-direction: column;
}

.avatar {
  border-radius: 50%;
  width: 80%;
}

.infos {
  color: white;
  font-size: 13px;

}

.link {
  background-color: #0368FF;
  border-radius: 2px;
  font-size: 13px;
  width: 150px;
  height: 30px;
  margin-top: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.title_login {
  font-size: 20px;
  font-weight: bold;
}

.bio {}

.repo {
  margin-top: 10px;
}
</style>
