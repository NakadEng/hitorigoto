<template>
  <div id="app">
    <MutterPost></MutterPost>
  </div>
</template>

<script>
import MutterPost from "./components/MutterPost.vue"
export default {
  name: 'app',
  data () { return {} },
  created: function() {},
  components: {
    MutterPost: MutterPost
  }
};
</script>