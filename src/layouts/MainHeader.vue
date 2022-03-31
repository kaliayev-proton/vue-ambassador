<template>
  <q-header elevated>
    <q-toolbar>
      <q-btn
        flat
        dense
        round
        icon="menu"
        aria-label="Menu"
        @click="toggleLeftDrawer()"
      />

      <q-toolbar-title> Quasar App </q-toolbar-title>

      <div class="flex items-center q-pa-md q-gutter-sm">
        <div>{{ user?.first_name }} {{ user?.last_name }}</div>

        <router-link to="/login">
          <q-btn color="purple" text-color="white" label="Login" />
        </router-link>
        <router-link to="/register">
          <q-btn color="amber" text-color="black" label="Register" />
        </router-link>
      </div>
    </q-toolbar>
  </q-header>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainHeader',
  props: ['user'],

  methods: {
    toggleLeftDrawer() {
      this.$emit('toggleLeftDrawer');
    },
  },
});
</script>
