<template>
  <div class="hello">

  </div>
</template>

<script>
export default {
  name: 'Tool',
  data() {
    return {
      config: {
        field1: 5,
        field2: '',
      },
      configFromBackend: {
        field1: 5,
        field2: 6,
      },
    };
  },
  methods: {
    emitEvent() {
      this.$emit('event-from-child-one', this.config);
    },
    onlyNumberImput(evt) {
         const charCode = evt.which ? evt.which : evt.keyCode;
         if (
            charCode > 31 &&
            (charCode < 48 || charCode > 57 || charCode == 46)

         ) {
            evt.preventDefault();
         }
      },
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
