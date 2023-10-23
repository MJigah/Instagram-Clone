<template>
  <q-page>
    <Header />
    <div class="xs column" style="height: 100vh">
      <AddPost />
    </div>
    <Footer />
  </q-page>
</template>

<script>
import Header from "../components/Header.vue";
import Footer from "../components/Footer.vue";
import AddPost from "../components/AddPost.vue";

export default {
  name: "CreatePage",
  components: { Header, Footer, AddPost },
};
</script>

<style lang="scss" scoped>
a {
  text-decoration: none;
  color: black;
}
.custom-border {
  border: 1px solid red;
}
</style>
