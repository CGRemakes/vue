<template>
  <div>
    <div v-if="isLoading">Loading games...</div>
    <div v-else>
      <table class="table">
        <thead>
          <tr>
            <th>Game Date</th>
            <th>BYU Score</th>
            <th>Utah Score</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <game-element
            v-for="game in games"
            :game="game"
            :key="game.id"
            @remove="removeGame(game.id)"
            @change="updateGame(game.id)"
          ></game-element>
        </tbody>
      </table>
      <game-form v-on:add="addGame"></game-form>
    </div>
  </div>
</template>

<script>
import { API_BASE_URL } from "../config";
import GameForm from "../components/GameForm.vue";
import GameElement from "../components/Game.vue";

export default {
  components: {
    "game-form": GameForm,
    "game-element": GameElement
  },
  data() {
    return {
      isLoading: true,
      games: {}
    };
  },
  created() {
    this.getGames();
  },
  methods: {
    getGames() {
      try {
        this.$http.get(API_BASE_URL + "/victories").then(response => {
          this.games = response.data.data;
          this.isLoading = false;
        });
      } catch (e) {
        console.log(e);
      }
    },
    removeGame(id) {
      try {
        this.$http.delete(API_BASE_URL + "/victories/" + id).then(response => {
          let index = this.games.map(item => item.id).indexOf(id);
          this.games.splice(index, 1);
          console.log(response);
        });
      } catch (e) {
        console.log(e);
      }
    },
    addGame(data) {
      try {
        this.$http.post(API_BASE_URL + "/victories", data).then(response => {
          this.games.push(response.data.data);
          data.game_date = "";
          data.byu_score = "";
          data.utah_score = "";
        });
      } catch (e) {
        console.log(e);
      }
    },
    updateGame(id) {
      let index = this.games.map(item => item.id).indexOf(id);
      let data = this.games[index];

      try {
        this.$http
          .post(API_BASE_URL + "/victories/" + id, data)
          .then(response => {
            console.log(response);
          });
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
  border: 1px solid black;
}
th {
  border: 1px solid black;
}
</style>
