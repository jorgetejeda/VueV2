<template>
  <div id="App">
    <p>Mensaje Original Largo: {{ message }}</p>
    <p>Mensaje Original Largo: {{ message.split("").reverse().join("") }}</p>
    <p>
      Mensaje Invertido Computado: {{ reversedMessage }}
      <br />
      <small
        >Se ejecutara una sola vez y se almacenara en cache esta cambiara solo
        caundo su dependencia original cambie</small
      >
    </p>
    <p>
      Mensaje Invertido Metodo: {{ handleReverseMessage() }}
      <br />
      <small>Se estara ejecutando cada vez que cambie la pagina</small>
    </p>
    <hr />
    <p>Observador (Computed): {{ fullNameComputed }}</p>
    <p>Observador Imperativo (Watch): {{ firstName }}</p>
    <p>Observador Get Set: {{ (getSetFullName = "Jorge Tejeda") }}</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    message: "anitalavalatina",
    firstName: "Foo",
    lastName: "Bar",
  }),
  computed: {
    reversedMessage: function () {
      return this.message.split("").reverse().join("");
    },
    fullNameComputed: function () {
      return this.firstName + " " + this.lastName;
    },
    getSetFullName: {
      get: function () {
        return this.firstName + " " + this.lastName;
      },
      set: function (value) {
        var names = value.split(" ");
        this.firstName = names[0];
        this.lastName = names[names.length - 1];
      },
    },
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + " " + this.lastName;
    },
    lastName: function (val) {
      this.fullName = this.firstName + " " + val;
    },
  },
  methods: {
    handleReverseMessage: function () {
      return this.message.split("").reverse().join("");
    },
  },
};
</script>>
