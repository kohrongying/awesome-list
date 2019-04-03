<template>
  <fragment v-on:close-modal="this.open = false">
    <md-button @click="onPress" class="md-icon-button menu-button">
      <md-icon v-if="open">close</md-icon>
      <md-icon v-else>menu</md-icon>
    </md-button>
    <NavMenu v-show="open" @clicked="handleClose" />
  </fragment>
</template>

<style>
.menu-button {
  box-shadow: 1px 1px 18px 0 #00000050;
  margin: 50px;
  z-index: 100;
  background-color: white;
}
</style>

<script lang="ts">
import Vue from "vue";
import { db, provider } from "../main";
import firebase from "firebase";
import "vue-material/dist/vue-material.min.css";
import { MdButton, MdIcon } from "vue-material/dist/components";
import { Fragment } from "vue-fragment";
import NavMenu from "@/components/NavMenu.vue"; // @ is an alias to /src

export default Vue.use(MdButton)
  .use(MdIcon)
  .extend({
    name: "NavButton",
    components: {
      Fragment,
      NavMenu
    },
    data() {
      return {
        authUser: "",
        open: false
      };
    },
    methods: {
      onPress() {
        console.log("click button");

        this.open = this.open ? false : true;
      },
      handleClose() {
        this.open = false;
      }
    }
  });
</script>
