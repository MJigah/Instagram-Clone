<template>
    <q-card
    v-if="step === 'step-1'"
    style="height: 800px;"
    :style="$q.screen.xs ? 'width: 100%' : 'width: 500px' "
  >
    <q-card-section class="row items-center q-pb-none">
      <div class="text-h6">Create New Post</div>
      <q-space />
      <q-btn icon="close" v-show="!$q.screen.xs" flat round dense v-close-popup />
    </q-card-section>

    <q-card-section
      class="flex items-center justify-between q-pa-md"
      style="height: 70px"
    >
      <q-file
        class="q-pa-none"
        style="width: 250px"
        @input="previewImage"
        type="file"
        clearable
        color="blue"
        standout
        bottom-slots
        @clear="resetImage"
        v-model="fileUpload"
        label="Upload Image"
        counter
      >
        <template v-slot:prepend>
          <q-icon name="attach_file" />
        </template>
      </q-file>
      <q-btn label="Next" @click="nextStep" />
    </q-card-section>
    <q-card-section
      v-if="preview"
      style="width: 100%; margin-top: 40px"
      class="flex items-center justify-center"
    >
      <img
        :src="preview"
        style="width: 400px; height: auto; object-fit: cover"
        class="img-fluid"
      />
      <div
        class="flex items-center justify-between q-mx-md"
        style="width: 100%"
      >
        <p class="mb-0">file name: {{ image.name }}</p>
        <p class="mb-0">size: {{ image.size / 1024 }}KB</p>
      </div>
    </q-card-section>
  </q-card>
  <q-card
    v-else-if="step === 'step-2'"
    style="height: 800px;"
    :style="$q.screen.xs ? 'width: 100%' : 'width: 500px' "
  >
    <q-card-section class="row items-center q-pb-none">
      <div class="text-h6 text-black">
        <q-icon
          class="cursor-pointer"
          name="keyboard_backspace"
          @click="prevStep"
          size="2rem"
        />
      </div>
      <q-space />
      <q-btn icon="close" v-show="!$q.screen.xs" flat round dense v-close-popup />
    </q-card-section>
    <q-card-section>
      <q-input
        class="q-my-md"
        outlined
        v-model="caption"
        label="Caption"
      />
      <q-input
        class="q-my-md"
        outlined
        v-model="location"
        label="Location"
      />
      <q-circular-progress
      v-if="userLoading"
      indeterminate
      rounded
      size="32px"
      color="blue"
      style="width: 100%"
      class="q-my-md flex justify-center"
      />
      <q-btn
      v-else
        class="q-my-md"
        style="width: 100%"
        outline
        color="primary"
        @click="postUpload"
        label="Post"
      />
    </q-card-section>
  </q-card>
</template>

<script>
import { ref, onMounted } from "vue";
import { useUserStore } from "stores/user";
import { storeToRefs } from "pinia";
import { useQuasar } from "quasar";

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

export default{
  setup(){
    return {
      dialog,
      fileUpload,
      image,
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


<style lang="scss" scoped>

</style>