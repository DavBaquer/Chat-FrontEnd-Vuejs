<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="row">
      <div class="col-12 col-md-4">
        <img  src="../assets/tecnologia1.png" />
      </div>
      <div  class="col-12 col-md-4">
        <img  src="../assets/tecnologia2.png" />
      </div>
      <div class="col-12 col-md-4">
        <img  src="../assets/tecnologia3.png" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeChat",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello img{
  width: 100%;
}
</style>
