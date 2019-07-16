<template>
  <div>
    <b-table striped hover :items="items"></b-table>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  data() {
    return {
      items: []
    };
  },
  mounted() {
    axios
      .get("http://localhost:4000/words")
      .then(response => {
        this.items = response.data;
      })
      .catch(function(error) {
        // handle error
        console.log(error);
      })
      .finally(function() {
        // always executed
      });
  }
};
</script>