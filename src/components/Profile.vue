<script lang="ts" setup>
const props = defineProps({
  profile: {
    type: Object,
    required: true
  }
});
</script>

<template>
  <figure class="profile">
    <img class="profile-photo" :src="props.profile.photo" alt="" width="300" height="512">
    <div class="profile-details">
      <blockquote>
        <p class="profile-quote font-medium">
          {{ props.profile.quote }}
        </p>
      </blockquote>
      <figcaption class="font-medium">
        <div class="text-sky-500">
          {{ props.profile.username }}
        </div>
      </figcaption>
    </div>
  </figure>
</template>

<style scoped>
.profile {
  --tw-ring-inset: ;
  --tw-ring-offset-width: 0px;
  --tw-ring-color: #3b82f680;
  --tw-bg-opacity: 1;
  display: flex;
  overflow: hidden;
  padding: 0;
  justify-content: center;
  border-radius: 0.75rem;
  box-shadow: var(--tw-ring-inset) 0 0 0 calc(1px + var(--tw-ring-offset-width)) var(--tw-ring-color);
  --un-bg-opacity: 1;
  background-color:rgb(30 41 59/var(--tw-bg-opacity));
}


.profile-photo {
  border-radius: 0;
  width: 12rem;
  height: auto;
}

.profile-details {
  margin-top: 1rem;
  padding: 2rem;
  text-align: left;
}
.font-medium {
  font-weight: 500;
}
.profile-quote {
  font-size: 1.125rem;
  line-height: 1.75rem;
}

.text-sky-500 {
  --un-text-opacity: 1;
  color: rgba(14, 165, 233, var(--un-text-opacity));
}

</style>
