<template>
  <div>
    {{ result }}
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group id="input-group-1" label="Palavra 1" label-for="input-1">
        <b-form-input id="input-1" v-model="form.word1" type="text" required></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-1" label="Palavra 2" label-for="input-1">
        <b-form-input id="input-1" v-model="form.word2" type="text" required></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Consultar</b-button>
      <b-button type="reset" variant="danger">Limpar</b-button>
    </b-form>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  data() {
    return {
      form: {
        word1: "",
        word2: "",
      },
      result: ""
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      axios
        .post("http://localhost:4000/words", {
          word1: this.form.word1,
          word2: this.form.word2
        })
        .then(response => {
          this.result = response.data
          console.log(response.data)
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    onReset(evt) {
      evt.preventDefault();
      this.result = ""
      this.form.word1 = "";
      this.form.word2 = "";
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>