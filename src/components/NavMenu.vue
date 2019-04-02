<template>
  <div class="modal-bg">
    <div class="menu">
      <div>hello</div>
    </div>
  </div>
</template>

<style>
.modal-bg {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: #00000066;
  display: flex;
  justify-content: center;
  align-items: center;
}
.menu {
  width: 40%;
  height: 30%;
  background-color: white;
  z-index: 100;
}
</style>

<script lang="ts">
import Vue from "vue";
import { db, provider } from "../main";
import firebase from "firebase";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";

export default Vue.use(MdButton)
  .use(MdIcon)
  .extend({
    name: "NavMenu",
    data() {
      return {
        authUser: ""
      };
    },
    methods: {}
  });
</script>
