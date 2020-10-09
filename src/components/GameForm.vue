<template>
  <form @submit.prevent="onSubmit">
    <div class="field">
      <div class="control">
        <input
          class="input"
          type="date"
          placeholder="Enter game date"
          v-model="game_date"
          name="game_date"
        />
        <input
          class="input"
          type="number"
          placeholder="Enter BYU Score"
          v-model="byu_score"
          name="byu_score"
        />
        <input
          class="input"
          type="number"
          placeholder="Enter Utah Score"
          v-model="utah_score"
          name="utah_score"
        />
      </div>
    </div>

    <button class="button is-primary">Add Game</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      game_date: null,
      byu_score: null,
      utah_score: null
    };
  },
  methods: {
    onSubmit() {
      this.$emit("add", this.$data);
    }
  }
};
</script>

<style>
form {
  margin-top: 40px;
}
</style>
