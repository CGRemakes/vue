<template>
  <tr>
    <td>
      <input type="date" @change="onChange" v-model="game.game_date" />
    </td>
    <td>
      <input type="number" @change="onChange" v-model="game.byu_score" />
    </td>
    <td>
      <input type="number" @change="onChange" v-model="game.utah_score" />
    </td>
    <td><button @click="$emit('remove')">Remove</button></td>
  </tr>
</template>

<script>
export default {
  props: ["game"],
  methods: {
    onChange() {
      this.$emit("change");
    }
  }
};
</script>

<style>
td {
  border: 1px solid black;
}
</style>
