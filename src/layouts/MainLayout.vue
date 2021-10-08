<template>
  <q-layout view="hHh LpR fFf">
    <q-header bordered class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title class="logo"> {{ appName }} </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      show-if-above
      :width="200"
      :breakpoint="500"
      bordered
      content-class="bg-grey-3"
    >
      <q-scroll-area class="fit">
        <q-list>
          <template v-for="(menuItem, index) in menuList" :key="index">
            <q-item
              class="q-mt-md"
              clickable
              :active="menuItem.label === menuItem.label"
              :to="menuItem.page"
              v-ripple
            >
              <q-item-section avatar>
                <q-icon :name="menuItem.icon" />
              </q-item-section>
              <q-item-section>
                {{ menuItem.label }}
              </q-item-section>
            </q-item>
          </template>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import conf from "../../package.json";
export default {
  data() {
    return {
      appName: "",
      menuList: [
        {
          icon: "person_add",
          label: "Add Staff",
          page: "/",
        },
        {
          icon: "more_time",
          label: "Shifts",
          page: "shifts",
        },
        {
          icon: "sync_alt",
          label: "Transactions",
          page: "transactions",
        },
      ],
    };
  },
  mounted() {
    this.appName = conf.productName;
  },
};
</script>


<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Lobster+Two:ital@1&display=swap");
.logo {
  font-family: "Lobster Two", cursive;
}
</style>