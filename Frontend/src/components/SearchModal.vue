<template>
    <div class="flex" style="" :style="$q.screen.xs ? 'padding: 20px; text-align:center; height: 100%' : 'width: 100%; height: 600px;'">
        <div style="width: 100%">
          <p v-show="!$q.screen.xs" class="text-h4 q-pa-md">Search</p>
          <q-input
            color="black"
            filled
            v-model="search"
            label="Search"
          >
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </div>
        <div
          class="flex items-center justify-center"
          style="height: 100%; width: 100%"
        >
          <p class="text-caption">No Recent Searches</p>
        </div>
      </div>
</template>

<script>
import {ref} from "vue";
const search = ref("");
    export default {
        name: 'SearchModal', 
        setup(){
          return{
            search,  
          }
        }
    }
</script>

<style lang="scss" scoped>

</style>