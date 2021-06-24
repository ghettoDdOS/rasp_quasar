<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-bar>
        <div class="px-2 text-weight-bold">
          Расписание
        </div>
      </q-bar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout",

  data() {
    return {};
  }
};
</script>
