<template>
  <div class="card">
    <div class="card-header">
      <strong>{{Followers.length}}</strong> followers (追隨者)
    </div>
    <div class="card-body">
      <router-link
        v-for="Follower in Followers"
        :key="Follower.id"
        :to="{name:userProfile,params:{id:Follower.id}}"
      >
        <img :src="Follower.image" width="60" height="60" class="avatar mx-2" />
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    Followers: {
      type: Array,
      required: true
    }
  }
};
</script>