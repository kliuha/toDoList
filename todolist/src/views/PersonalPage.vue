<template>
  <div class="home">
    <NewListItem msg="Welcome to Your personal list" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import NewListItem from "../components/NewListItem.vue"; // @ is an alias to /src

@Component({
  components: {
    NewListItem,
  },
})
export default class Home extends Vue {}
</script>
