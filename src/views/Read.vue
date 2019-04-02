<template>
  <div class="read">
    <h1>Read</h1>
    <div v-for="item in items">
      <p>{{ item.item }}</p>
      <button @click="deleteItem(item)">
        Remove
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";
import { db } from "../main";

export default {
  name: "Read",
  data() {
    return {
      items: []
    };
  },
  firestore() {
    return {
      items: db.collection("read")
    };
  },
  methods: {
    deleteItem(item) {
      db.collection("read")
        .doc(item[".key"])
        .delete();
    }
  }
};
</script>
