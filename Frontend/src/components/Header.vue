<template>
  <q-header class="bg-white text-grey-10" bordered>
    <q-toolbar class="text-grey-10 constrain">
      <q-btn
        class="large-screen q-mr-sm"
        flat
        round
        icon="eva-camera-outline"
        size="20px"
        to="/camera"
      />
      <q-separator class="large-screen" vertical spaced />

      <q-toolbar-title class="text-grand-hotel text-bold text-teal-8">
        Instagram
      </q-toolbar-title>
      <q-btn
        v-show="$q.screen.xs"
        flat
        icon="logout"
        :onclick="logoutUser"
        label="Sign Out"
        size="10px"
      />
      <q-btn
        class="large-screen"
        flat
        round
        icon="eva-home-outline"
        size="20px"
        to="/"
      />
    </q-toolbar>
  </q-header>
</template>

<script>
import { useUserStore } from "stores/user";
import { storeToRefs } from "pinia";
const userStore = useUserStore(); // state and getters need "storeToRefs"
const { uploadPosts, reset, logoutUser } = userStore;
export default {
  name: "Header",
  setup() {
    return {
      logoutUser,
    };
  },
};
</script>

<style lang="scss" scoped>
.q-footer .q-tab__icon {
  font-size: 30px;
}
.q-toolbar__title {
  @media (max-width: $breakpoint-xs-max) {
    text-align: center;
  }
  @media (min-width: $breakpoint-sm-min) {
    height: 80px;
    display: flex;
    align-items: center;
  }
  font-size: 35px;
}

.q-toolbar a {
  @media (min-width: $breakpoint-sm-min) {
    // display: block;
    display: flex;
    align-items: center;
  }
}
</style>
