<template>
  <div
    class="flex"
    style=""
    :style="
      $q.screen.xs
        ? 'padding: 20px; text-align:center; height: 100%'
        : 'width: 100%; height: 600px;'
    "
  >
    <div style="width: 100%">
      <p v-show="!$q.screen.xs" class="text-h4 q-pa-md">Search</p>
      <q-input
        color="black"
        filled
        v-model="search"
        label="Search"
        @keyup="searchUser"
      >
        <template v-slot:append>
          <q-icon name="search" />
        </template>
      </q-input>
    </div>
    <div
      :class="{
        'flex items-center justify-center':
          recentSearch.length < 1 && userSearch < 0,
      }"
      style="height: 100%; width: 100%"
    >
      <div v-if="userSearch.length > 0" class="q-my-md">
        <ul v-for="user in userSearch" :key="user._id">
          <li class="search-li">
            <a href="#" class="q-pa-sm">
              {{ user.username }}
            </a>
          </li>
        </ul>
      </div>
      <p v-else-if="recentSearch.length < 1" class="text-caption">
        No Recent Searches
      </p>
      <div v-else>
        {{ recentSearch }}
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { useUserStore } from "stores/user";
import { storeToRefs } from "pinia";

const search = ref("");
const userStore = useUserStore();
const { userLoading, userSearch, recentSearch } = storeToRefs(userStore);
const { searchUserName, userReset } = userStore;
export default {
  name: "SearchModal",
  data() {
    return {
      search,
      userLoading,
      userSearch,
      recentSearch,
      searchUser: () => {
        if (search.value.length > 0) {
          searchUserName(search.value);
        }
      },
    };
  },
  unmounted: () => {
    search.value ="";
    userReset()
  }
};
</script>

<style lang="scss" scoped>
a {
  color: grey;
  text-decoration: none;
}

ul{
  margin: 0;
  padding: 0;
}

li {
  margin: 0;
  list-style-type: none;
}

.search-li{
  width: 100%;
  border-radius: 6px;
  margin: 8px 0;
}

.search-li a{
  display: inline-block;
  width: 100%;
  height: 100%;
  cursor: pointer;
  color: black;
  letter-spacing: .5px;
}

.search-li:hover{
  background-color: rgb(184, 184, 184);
}
</style>
