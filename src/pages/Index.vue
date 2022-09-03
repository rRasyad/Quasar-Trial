<template>
  <q-page padding>
    <button style="position: absolute; right: 10px" @click="counter++">
      {{ counter }}
    </button>

    <!-- <input v-model="message" @keyup="handleKeyup"/> -->

    <!-- <input v-model="message" 
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      @mouseenter="alertMessage"
    /> -->

    <!-- <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      v-bind:class="{ error: message.length > 23 }"
    /> -->

    <!-- <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :style="errorStyle"
      ref="messageInput"
    /> -->

    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :class="{ error: message.length > 23 }"
      ref="messageInput"
    />

    <button @click="clearMessage">Clear</button>

    <div>{{ message.length }}</div>

    <!-- <h5 
      v-show="message.length"
      class="border-grey">{{message}}</h5> -->

    <h5 v-if="message.length" class="border-grey">{{ message }}</h5>

    <h6 v-else>No message entered ❤</h6>

    <hr />

    <p>Uppercase message: {{ messageUppercase }}</p>
    <p>Lowercase message: {{ message | messageLowercase }}</p>
  </q-page>
</template>

<script>
//dari sananya
// import { defineComponent } from "vue";

// export default defineComponent({

// });
const autofocus = {
  inserted(el) {
    console.log("input inserted");
    el.focus();
  },
};

export default {
  data() {
    return {
      message: "I want to study Quasar!",
      counter: 0,
    };
  },
  computed: {
    messageUppercase() {
      console.log("messageUppercase was fired");
      return this.message.toUpperCase() + this.counter;
      //only computed can acces data
    },
    errorStyle() {
      if (this.message.length > 23) {
        return {
          color: "red",
          background: "pink",
        };
      }
    },
  },
  methods: {
    clearMessage() {
      this.message = "";
    },
    // handleKeyup(e){
    //   console.log(e)
    //   if (e.keyCode == 27) {
    //     this.clearMessage()
    //   } else if(e.keyCode == 13){
    //     this.alertMessage()
    //   }
    // },
    alertMessage() {
      alert(this.message);
    },
  },
  filters: {
    messageLowercase(value) {
      return value.toLowerCase();
    },
  },
  directives: {
    autofocus,
    // autofocus: {
    //   inserted(el) {
    //     console.log("input inserted");
    //     el.focus();
    //   },
    // },
  },
  // beforeCreate() {
  //   console.log("beforeCreate");
  // },
  // created() {
  //   console.log("created");
  // },
  // beforeMount() {
  //   console.log("beforeMount");
  // },
  mounted() {
    // console.log("mounted");

    //refs is not recomended
    console.log(this.$refs);
    this.$refs.messageInput.className = "bg-green";
  },
  // beforeUpdate() {
  //   console.log("beforeUpdated");
  // },
  // updated() {
  //   console.log("updated");
  // },
  // beforeDestroy() {
  //   console.log("beforeDestroy");
  // },
  // destroyed() {
  //   console.log("destroyed");
  // },
};
</script>

<style>
.border-grey {
  border: 1px solid grey;
}
input,
button {
  font-size: 23px;
}
.error {
  color: red;
  background: pink;
}
</style>
