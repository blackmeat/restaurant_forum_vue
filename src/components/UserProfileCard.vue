<template>
  <div class="card mb-3">
    <div class="row no-gutters">
      <div class="col-md-4">
        <img :src="User.image" width="300px" height="300px" />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h5 class="card-title">{{User.name}}</h5>
          <p class="card-text">{{User.email}}</p>
          <ul class="list-unstyled list-inline">
            <li>
              <strong>{{User.CommentsCount}}</strong> 已評論餐廳
            </li>
            <li>
              <strong>{{User.FavoritedRestaurantsCount}}</strong> 收藏的餐廳
            </li>
            <li>
              <strong>{{User.FollowingsCount}}</strong> followings (追蹤者)
            </li>
            <li>
              <strong>{{User.FollowersCount}}</strong> followers (追隨者)
            </li>
          </ul>
          <p>
            <a href="/users/1/edit">
              <button type="submit" class="btn btn-primary">edit</button>
            </a>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    User: {
      type: Object,
      require: true
    }
  }
};
</script>