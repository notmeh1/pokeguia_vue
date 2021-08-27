<template>
  <PokeGuia class="container" />
</template>

<script>
import PokeGuia from "./PokeGuia";
export default {
  components: {
    PokeGuia,
  },
};
</script>
<!-- Esto es para que no duelan los ojos -->
<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100;300;400;500;700&display=swap");
body {
  background-color: #1a202c;
  font-family: "Montserrat", sans-serif;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-items: center;
}
</style>
