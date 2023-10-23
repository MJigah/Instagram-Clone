<template>
  <q-card class="bg-transparent no-box-shadow no-shadow">
    <q-tabs
      v-model="tab"
      dense
      class="text-grey"
      :class="{ 'justify-around border-y': $q.screen.xs }"
      active-color="black"
      indicator-color="black"
      inline-label
      narrow-indicator
    >
      <q-tab
        :style="$q.screen.xs ? 'flex: 0;' : 'flex: 1'"
        name="posts"
        icon="grid_on"
        :label="!$q.screen.xs ? 'Posts' : ''"
      />
      <q-tab
        :style="$q.screen.xs ? 'flex: 0;' : 'flex: 1'"
        name="saved"
        icon="turned_in_not"
        :label="!$q.screen.xs ? 'Saved' : ''"
      />
      <q-tab
        :style="$q.screen.xs ? 'flex: 0;' : 'flex: 1'"
        name="tags"
        icon="portrait"
        :label="!$q.screen.xs ? 'Tagged' : ''"
      />
    </q-tabs>

    <q-tab-panels
      class="flex bg-transparent no-shadow no-box-shadow q-mx-md justify-center"
      v-model="tab"
      animated
    >
      <q-tab-panel name="posts">
        <div v-if="userLoading">
          <div class="row">
            <div class="col">
              <div class="">
                <q-card style="max-width: 300px">
                  <q-item>
                    <q-item-section avatar>
                      <q-skeleton type="QAvatar" />
                    </q-item-section>

                    <q-item-section>
                      <q-item-label>
                        <q-skeleton type="text" />
                      </q-item-label>
                      <q-item-label caption>
                        <q-skeleton type="text" />
                      </q-item-label>
                    </q-item-section>
                  </q-item>

                  <q-skeleton height="200px" square />

                  <q-card-actions align="right" class="q-gutter-md">
                    <q-skeleton type="QBtn" />
                    <q-skeleton type="QBtn" />
                  </q-card-actions>
                </q-card>
              </div>
            </div>
          </div>
        </div>
        <div v-else-if="userPosts.length > 0" class="row">
          <div
            v-for="post in userPosts"
            :key="post._id"
            class=" col-lg-3 col-md-3 col-xs-6"
          >
            <q-card class="my-card" flat bordered>
              <img :src="post.posts[0].url" />

              <q-card-actions align="right">
                <q-btn flat round color="red" icon="favorite" />
                <q-btn flat round color="teal" icon="bookmark" />
                <q-btn flat round color="primary" icon="share" />
              </q-card-actions>
            </q-card>
          </div>
        </div>
        <div v-else class="q-ma-md text-center">You have No Posts!</div>
      </q-tab-panel>

      <q-tab-panel class="bg-transparent no-shadow no-box-shadow" name="saved">
        <div class="row" v-if="user?.savedPosts?.length > 0">
          <div class="col">.col</div>
          <div class="col">.col</div>
          <div class="col">.col</div>
        </div>
        <div v-else class="row">
            No Saved Posts
        </div>
      </q-tab-panel>

      <q-tab-panel class="bg-transparent no-shadow no-box-shadow" name="tags">
        <div class="row">
          <div class="col">.col</div>
          <div class="col">.col</div>
          <div class="col">.col</div>
        </div>
      </q-tab-panel>
    </q-tab-panels>
  </q-card>
</template>

<script>
import { ref } from "vue";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";

const userStore = useUserStore();
const { user, userPosts, userLoading } = storeToRefs(userStore);
const { fetchUserDetails, fetchUserPosts, userReset } = userStore;
const tab = ref("posts");
export default {
  setup() {
    return {
      tab,
      user,
      userPosts,
      userLoading,
    };
  },
};
</script>

<style lang="scss">
.border-y{
  border-top: 1px solid rgb(191, 191, 191) !important;
  border-bottom: 1px solid rgb(191, 191, 191) !important;
}

.q-tabs--not-scrollable .q-tabs__content {
  justify-content: space-evenly;
}
</style>
