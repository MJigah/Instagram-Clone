<template>
  <q-page>
    <q-page class="xs">
      <div class="column" style="height: 100vh">
        <div class="col-5">
          <div class="column" style="height: 100%">
            <div class="col-2 flex align-center justify-center">
              <div class="row q-py-lg" style="width: 100%">
                <div class="col-7 text-right text-weight-medium">
                  <q-icon name="lock" />
                  {{ user?.username }}
                  <q-icon name="keyboard_arrow_down" />
                </div>
                <div class="col-5 text-right q-px-md">
                  <q-icon name="menu" />
                </div>
              </div>
            </div>
            <div class="col-3">
              <div class="row">
                <div class="col-4 flex align-center justify-center">
                  <div
                    class="border-rad flex items-center justify-center q-pa xs"
                  >
                    <q-avatar size="4rem">
                      <img src="https://cdn.quasar.dev/img/avatar.png" />
                    </q-avatar>
                  </div>
                </div>
                <div class="col">
                  <div class="column flex items-center justify-center">
                    <div class="col text-weight-medium">{{ userPosts?.length}}</div>
                    <div class="col text-weight-light text-caption">Posts</div>
                  </div>
                </div>
                <div class="col">
                  <div class="column flex items-center justify-center">
                    <div class="col text-weight-medium">{{ user?.followers && user?.followers.length}}</div>
                    <div class="col text-weight-light text-caption">
                      Followers
                    </div>
                  </div>
                </div>
                <div class="col">
                  <div class="column flex items-center justify-center">
                    <div class="col text-weight-medium">{{ user?.followings && user?.followings.length}}</div>
                    <div class="col text-weight-light text-caption">
                      Following
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-4 q-mx-md flex items-center">
              <div class="column" style="width: 100%;">
                <div class="col text-caption">{{ user?.bio }}</div>
                <q-btn
                  size=".7rem"
                  no-caps
                  outline
                  class="q-my-sm border-grey"
                  text-color="black"
                  dense
                  label="Edit Profile"
                />
              </div>
            </div>
            <div class="col">
              <q-scroll-area
                :visible="false"
                style="height: 90px; max-width: 98%"
              >
                <div class="row no-wrap q-my-xs q-mx-md">
                  <div class="col q-mx-sm q-mx-md">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-icon name="add" color="grey" size="2.4rem" />
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                  <div class="col q-mx-sm">
                    <div
                      class="border-rad flex items-center justify-center q-pa xs"
                    >
                      <q-avatar size="4rem">
                        <img src="https://cdn.quasar.dev/img/avatar.png" />
                      </q-avatar>
                    </div>
                  </div>
                </div>
              </q-scroll-area>
            </div>
          </div>
        </div>
        <div class="col-7 q-py-md">
          <PostsTab />
        </div>
      </div>
      <Footer />
    </q-page>
    <q-page class="md">
      <div class="row" style="height: 100vh">
        <div
          class="col-2 q-px-md q-py-xl"
          style="border-right: 1px solid rgb(211, 211, 211)"
        >
          <Search />
        </div>
        <div class="col">
          <div class="column" style="height: 100%">
            <div
              class="col-5 flex items-center justify-center"
              style="width: 100%"
            >
              <div class="row" style="width: 65%; height: 300px">
                <div class="col flex items-center justify-center">
                  <div class="" style="">
                    <q-avatar size="170px">
                      <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
                    </q-avatar>
                  </div>
                </div>
                <div class="col q-pa-lg">
                  <div>
                    <div
                      class="flex items-center justify-between"
                      style="width: 250px"
                    >
                      <a class="custom-link text-body1" href="#">{{
                        user?.username
                      }}</a>
                      <q-btn
                        class="q-px-md text-body1"
                        color="grey"
                        dense
                        no-shadow
                        no-caps
                        label="Edit Profile"
                      />
                      <q-icon size="1.7rem" name="settings" />
                    </div>
                    <div class="q-my-lg flex items-center justify-between">
                      <p style="margin: 0">{{ userPosts.length }} posts</p>
                      <a class="custom-link" href="#"
                        >{{
                          user.followers && user?.followers.length
                        }}
                        followers</a
                      >
                      <a class="custom-link" href="#"
                        >{{
                          user.followings && user?.followings.length
                        }}
                        followings</a
                      >
                    </div>
                  </div>
                  <div class="q-my-lg">
                    <p>{{ user?.name }}</p>
                    <p>{{ user?.website }}</p>
                    <p>{{ user?.bio }}</p>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-5 custom-border-top">
              <PostsTab />
            </div>
          </div>
        </div>
      </div>
    </q-page>
  </q-page>
</template>

<script>
import Footer from "../components/Footer.vue";
import Search from "../components/Search.vue";
import PostsTab from '../components/PostsTab.vue';
import { ref } from "vue";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

const userStore = useUserStore();
const { user, userPosts, userLoading } = storeToRefs(userStore);
const { fetchUserDetails, fetchUserPosts, userReset } = userStore;
export default {
  name: "DashboardPage",
  components: {
    Footer,
    Search,
    PostsTab,
  },
  data() {
    return {
      user,
      userPosts,
      userLoading,
    };
  },
  mounted() {
    fetchUserDetails();
  },
  unmounted() {
    userReset();
  },
  created(){
    fetchUserPosts();
  }
};
</script>

<style lang="scss">
.border-grey {
  border-block-color: black;
}

.q-tab__content {
  width: 100%;
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
}

.q-tab__content p {
  margin: 0;
  margin-left: 10px;
  text-align: left;
}

.border-rad {
  height: 4.5rem;
  width: 4.5rem;
  border: 2px solid grey;
  border-radius: 50%;
}

.custom-border {
  border: 1px solid red;
}

.custom-border-right {
  border-right: 1px solid black;
}

.custom-border-top {
  border-top: 1px solid rgb(180, 180, 180);
}

.custom-link {
  color: black;
  text-decoration: none;
}
</style>
