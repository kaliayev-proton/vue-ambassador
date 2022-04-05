<template>
  <q-layout view="lHh Lpr lFf">
    <MainHeader
      :user="user"
      @toggleLeftDrawer="toggleLeftDrawer"
      @logout="logout"
    />

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <MainNav />
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { api } from 'src/boot/axios';
import { defineComponent } from 'vue';
import { useRouter } from 'vue-router';
import MainNav from './MainNav.vue';
import MainHeader from './MainHeader.vue';
import { User } from 'src/models/user';

export default defineComponent({
  name: 'MainLayout',

  components: {
    MainNav,
    MainHeader,
  },

  data() {
    return {
      user: new User(),
      leftDrawerOpen: false,
    };
  },
  methods: {
    toggleLeftDrawer() {
      this.leftDrawerOpen = !this.leftDrawerOpen;
    },
    async logout() {
      await api.post('logout');

      this.$router.push('login');
    },
  },

  setup() {
    // const leftDrawerOpen = ref(false);
    // return {
    //   leftDrawerOpen: this.leftDrawerOpen,
    // };
  },
  async mounted() {
    const router = useRouter();
    try {
      const { data } = await api.get('user');
      this.user = data;
    } catch {
      router.push('login');
    }
  },
});
</script>
