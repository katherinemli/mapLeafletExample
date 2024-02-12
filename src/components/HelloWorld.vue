<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      With an eye for intuitive, well designed and user-friendly websites, I love to build websites that not only look great, but also feel great to use, regardless.
    </p>
    <ul>
      <li><a href="https://github.com/katherinemli" target="_blank" rel="noopener">Github Portfolio</a></li>
      <li><a href="https://www.linkedin.com/in/katherine-liberona-irarrazabal-76a843150/" target="_blank" rel="noopener">Linkedin Profile</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
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
</style>
