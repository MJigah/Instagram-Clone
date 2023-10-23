<template>
  <div>
    <div class="">
      <div class="q-py-md" style="height: 100vh; width: 100%">
        <a v-show="!$q.screen.sm" class="text-grand-hotel text-bold text-h4 custom-link" href="#"
          >Instagram</a
        >
        <q-tabs v-model="tab" vertical class="text-black q-pt-lg">
          <div class="column" style="height: 100%">
            <div class="col-10">
              <a href="#/" class="custom-link">
                <q-tab class="flex flex-row" name="home" icon="home">
                  <p v-show="!$q.screen.sm" class="text-caption">home</p>
                </q-tab>
              </a>
              <q-tab name="search" icon="search" @click="open('left')">
                <p v-show="!$q.screen.sm" class="text-caption">search</p>
              </q-tab>
              <q-tab name="add_box" icon="add_box" @click="addPost = true">
                <p v-show="!$q.screen.sm" class="text-caption">Create</p>
              </q-tab>
              <a href="#/home" class="custom-link">
                <q-tab name="perm_identity" icon="perm_identity">
                  <p v-show="!$q.screen.sm" class="text-caption">Profile</p>
                </q-tab>
              </a>
              <q-dialog v-model="dialog" :position="position">
                <q-card style="width: 350px; height: 100vh">
                  <!-- <q-linear-progress :value="0.6" color="pink" /> -->
    
                  <q-card-section class="row items-center no-wrap">
                    <SearchModal />
                  </q-card-section>
                </q-card>
              </q-dialog>
              <q-dialog v-model="addPost">
                  <AddPost />
              </q-dialog>
            </div>
            <div class="col">
              <q-btn :onClick="logoutUser" color="blue" label="Logout"/>
            </div>
          </div>
        </q-tabs>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { useUserStore } from "stores/user";
import { storeToRefs } from "pinia";
import { useQuasar } from "quasar";
import AddPost from "./AddPost.vue";
import SearchModal from "./SearchModal.vue";

const $q = useQuasar();
const userStore = useUserStore();
const {
  user,
  getUserDetails,
  userLoading,
  userSuccess,
  userError,
  userMessage,
} = storeToRefs(userStore); // state and getters need "storeToRefs"
const { uploadPosts, reset, logoutUser } = userStore;
const dialog = ref(false);
const fileUpload = ref(null);
const image = ref(null);
const preview = ref(null);
const commentDialog = ref(false);
const addPost = ref(false);
const position = ref("left");
const text = ref("");
const search = ref("");
const stepState = ref(1);
const step = ref("step-1");
const caption = ref("Meeeeeeeeeeeee");
const location = ref("Nigeria");
const tab = ref("");

export default{
  components: { AddPost, SearchModal },
  setup(){
    return {
      dialog,
      fileUpload,
      image,
      tab,
      preview,
      commentDialog,
      addPost,
      position,
      text,
      search,
      stepState,
      step,
      caption,
      location,
      userLoading,
      logoutUser,
      open: (pos) => {
        position.value = pos;
        dialog.value = true;
      },
      previewImage : (event) => {
        var input = event.target;
        if (input.files) {
          var reader = new FileReader();
          reader.onload = (e) => {
            preview.value = e.target.result;
          };
          image.value = input.files[0];
          reader.readAsDataURL(input.files[0]);
        }
      },
      resetImage: () => {
        image.value = null;
        preview.value = null;
      },
      nextStep: () => {
        stepState.value = stepState.value + 1;
        step.value = `step-${stepState.value}`;
      },
      prevStep: () => {
        stepState.value = stepState.value - 1;
        step.value = `step-${stepState.value}`;
      },
      postUpload: async () => {
        if(caption.value === "" || location.value === ""){
          $q.notify({
            message: 'Enter Missing Fields!',
            color: "red",
          });
        } else {
          let formdata = new FormData();
          formdata.append("posts", fileUpload.value);
          formdata.append("caption", caption.value);
          formdata.append("location", location.value);
          await uploadPosts(formdata);
          if (userSuccess && userMessage) {
            $q.notify({
              message: userMessage.value,
              color: "green",
            });
          }
        }
      },
    
    }
  }
}
</script>

<style lang="scss" scoped></style>
