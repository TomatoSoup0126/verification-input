<script setup lang="ts">
import { computed, reactive, ref, onMounted } from 'vue';
import OtpVerify from '@/components/OtpVerify.vue'
import Profile from '@/components/Profile.vue'
import Loading from '@/components/Loading.vue'

const isLoading = ref(false);
const token = ref('');
const user = reactive({
  profile: {
    photo: '',
    quote: '',
    username: ''
  }
});

const handleLoading = (value) => {
  isLoading.value = value;
}

const showOtpVerify = computed(() => {
  return Object.values(user.profile).every((value) => value === '') && !token.value;
});

const postAuth = async () => {
  handleLoading(true);
  try {
    const response = await fetch('/api/auth', {
      headers: {
        'Authorization': token.value
      },
    })
    const data = await response.json();
    if (data) {
      user.profile = data;
    }
  } catch (error) {
    console.error(error);
  } finally {
    handleLoading(false);
  }
};


const handleUpdateToken = (value) => {
  token.value = value;
  saveTokenToLocalStorage()
  postAuth();
};

const saveTokenToLocalStorage = () => {
  localStorage.setItem('token', token.value);
};

const getTokenFromLocalStorage = () => {
  const token = localStorage.getItem('token');
  if (token) {
    handleUpdateToken(token);
  }
};

const handleLogout = () => {
  token.value = '';
  user.profile = {
    photo: '',
    quote: '',
    username: ''
  };
  localStorage.removeItem('token');
};

onMounted(() => {
  getTokenFromLocalStorage();
});
</script>

<template>
  <Loading v-if="isLoading"/>
  <Profile
    v-if="!showOtpVerify"
    :profile="user.profile"
    @logout="handleLogout"
  />
  <OtpVerify
    v-else
    @start-loading="handleLoading(true)"
    @stop-loading="handleLoading(false)"
    @update-token="handleUpdateToken"
  />
</template>
