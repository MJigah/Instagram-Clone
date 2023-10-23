<template>
  <q-page>
    <Header />
    <div class="xs column" style="height: 100vh">
      <SearchModal />
    </div>
    <Footer />
  </q-page>
</template>

<script>
import Footer from "../components/Footer.vue";
import Header from "../components/Header.vue";
import SearchModal from "../components/SearchModal.vue";
export default {
  name: "SearchPage",
  components: {
    Header,
    Footer,
    SearchModal,
  },
  setup () {

    return {
    }
  }
};
</script>

<style lang="sass" scoped>
a 
  text-decoration: none


.border-1 
  border: 1px solid black
  color: black


.example-masonry
  .flex-break
    flex: 1 0 100% !important
    width: 0 !important

  $x: 4

  @for $i from 1 through ($x - 1)
    .example-container > div:nth-child(#{$x}n + #{$i})
      order: #{$i}

  .example-container > div:nth-child(#{$x}n)
    order: #{$x}

  .example-container
    height: 50rem

    .example-cell
      width: 25%
      padding: 1px

      > div
        padding: 4px 8px
        box-shadow: inset 0 0 0 2px #9e9e9e
</style>
