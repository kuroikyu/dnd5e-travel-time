<template>
  <!-- <HelloWorld msg="Hello Vue 3 in CodeSandbox!" /> -->
  <TravelInput />
</template>

<script>
// import HelloWorldVue from "./components/HelloWorld.vue";
// import "normalize.css";
import TravelInput from "./components/TravelInput.vue";

export default {
  name: "App",
  components: {
    // HelloWorld: HelloWorldVue,
    TravelInput: TravelInput,
  },
};
</script>