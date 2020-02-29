<template >
  <div class="row">
    <div class="col-md-6 col-lg-4" v-for="restaurant in restaurants" :key="restaurant.id">
      <div class="card mb-4">
        <img
          class="card-img-top"
          :src="restaurant.image"
          alt="Card image cap"
          width="286px"
          height="180px"
        />
        <div class="card-body">
          <p class="card-text title-wrap">
            <a href="#">{{ restaurant.name }}</a>
          </p>
          <!-- <span class="badge badge-secondary">{{ restaurant.Category.name }}</span> -->
          <p class="card-text text-truncate">{{ restaurant.description }}</p>
        </div>
        <div class="card-footer">
          <button type="button" class="btn btn-danger btn-border favorite mr-2">移除最愛</button>
          <button type="button" class="btn btn-primary btn-border favorite mr-2">加到最愛</button>
          <button type="button" class="btn btn-danger like mr-2">Unlike</button>
          <button type="button" class="btn btn-primary like mr-2">Like</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    initialRestaurant: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      restaurants: this.initialRestaurant
    };
  }
};
</script>