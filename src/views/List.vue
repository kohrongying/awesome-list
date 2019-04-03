<template>
  <div class="read">
    <h1 class="title">{{ this.$route.params.list }}</h1>
    <div v-for="(item, index) in items" :key="index" class="action-item">
      <p>{{ item.name }}</p>
      <md-button @click="deleteItem(item)" class="md-icon-button">
        <md-icon>close</md-icon>
      </md-button>
    </div>
  </div>
</template>

<style scoped>
.title {
  font-size: xx-large;
}

.action-item {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 60vw;
  font-size: large;
}
</style>
<script lang="ts">
import Vue from "vue";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";
import { db } from "../main";
import firebase from "firebase";

export default Vue.use(MdButton)
  .use(MdIcon)
  .extend({
    name: "Read",
    data() {
      return {
        items: [],
        uid: ""
      };
    },
    created() {
      this.uid = firebase.auth().currentUser.uid;

      const userRef = db.collection("users").doc(`${this.uid}`);
      userRef.get().then(doc => {
        this.items = doc.data()[this.$route.params.list];
        console.log(doc.data()["read"]);
      });
    },
    methods: {
      deleteItem(item) {
        // db.collection("read")
        //   .doc(item[".key"])
        //   .delete();
      }
    }
  });
</script>
