<template>
  <q-layout view="lHh Lpr lFf" class="bg-primary">
    <q-img
      src="background.jpg"
      :ratio="16 / 9"
      spinner-color="primary"
      spinner-size="82px"
      class="fit absolute"
    />

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
