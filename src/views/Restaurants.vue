<template>
  <div class="container py-5">
    <Navtab />
    <!-- 餐廳類別標籤 RestaurantsNavPills -->
    <RestaurantsNavPills :categories="categories" />
    <div>
      <!-- 餐廳卡片 RestaurantCard-->
      <div class="row">
        <RestaurantCard
          v-for="restaurant in restaurants"
          :key="restaurant.id"
          :initial-restaurant="restaurant"
        />
      </div>
    </div>

    <!-- 分頁標籤 RestaurantPagination -->
    <RestaurantsPagination
      v-if="totalPage > 1"
      :category-id="categoryId"
      :current-page="currentPage"
      :total-page="totalPage"
    />
  </div>
</template>

<script>
import Navtab from "./../components/Navtab";
import RestaurantCard from "../components/RestaurantCard";
import RestaurantsNavPills from "../components/RestaurantsNavPills";
import RestaurantsPagination from "../components/RestaurantsPagination";

const dummyData = {
  restaurants: [
    {
      id: 51,
      name: "發大財0121牛排",
      tel: "12345678",
      address: "高雄市",
      opening_hours: "00:00",
      description: "123",
      image: "https://i.imgur.com/CaeM9rg.jpg",
      viewCounts: 27,
      createdAt: "2019-11-22T06:50:58.472Z",
      updatedAt: "2020-02-11T03:49:29.072Z",
      CategoryId: 6,
      Category: {
        id: 6,
        name: "美式料理",
        createdAt: "2019-11-20T06:25:42.917Z",
        updatedAt: "2019-11-20T06:25:42.917Z"
      },
      isFavorited: false,
      isLiked: true
    },
    {
      id: 14,
      name: "Rahul Kilback",
      tel: "1-573-027-3190",
      address: "13538 Lula Roads",
      opening_hours: "08:00",
      description: "Ut ea repellat cumque illo sint. Possimus a magni ",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=66.19683181847653",
      viewCounts: 77,
      createdAt: "2019-11-20T06:25:42.925Z",
      updatedAt: "2020-02-16T05:36:07.120Z",
      CategoryId: 7,
      Category: {
        id: 7,
        name: "複合式料理",
        createdAt: "2019-11-20T06:25:42.917Z",
        updatedAt: "2019-11-20T06:25:42.917Z"
      },
      isFavorited: true,
      isLiked: true
    },
    {
      id: 30,
      name: "Vince Kassulke",
      tel: "(302) 097-9821 x641",
      address: "82815 Vivianne Inlet",
      opening_hours: "08:00",
      description: "nihil",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=60.72153192006735",
      viewCounts: 112,
      createdAt: "2019-11-20T06:25:42.928Z",
      updatedAt: "2020-02-16T05:35:03.543Z",
      CategoryId: null,
      Category: null,
      isFavorited: false,
      isLiked: false
    },
    {
      id: 29,
      name: "Mrs. Deonte Schmeler",
      tel: "694-889-1934",
      address: "4833 Ila Causeway",
      opening_hours: "08:00",
      description: "Ut officia pariatur quam perferendis quia nihil ex",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=33.27090568354101",
      viewCounts: 9,
      createdAt: "2019-11-20T06:25:42.928Z",
      updatedAt: "2020-02-16T05:35:11.396Z",
      CategoryId: null,
      Category: null,
      isFavorited: false,
      isLiked: false
    },
    {
      id: 24,
      name: "Tracy Kling",
      tel: "602.671.9831",
      address: "4776 Hazle Freeway",
      opening_hours: "08:00",
      description: "Libero fugit omnis inventore quasi maxime magnam a",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=28.34397872340968",
      viewCounts: 6,
      createdAt: "2019-11-20T06:25:42.927Z",
      updatedAt: "2020-02-16T05:34:58.076Z",
      CategoryId: null,
      Category: null,
      isFavorited: false,
      isLiked: false
    },
    {
      id: 26,
      name: "Dayna Roberts",
      tel: "759-389-2695",
      address: "9850 Kaia Circle",
      opening_hours: "08:00",
      description: "ipsum",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=3.7178880115385837",
      viewCounts: null,
      createdAt: "2019-11-20T06:25:42.928Z",
      updatedAt: "2019-11-20T06:25:42.928Z",
      CategoryId: null,
      Category: null,
      isFavorited: true,
      isLiked: false
    },
    {
      id: 34,
      name: "Frida Jones",
      tel: "(605) 542-9140 x08706",
      address: "5248 Dare Forge",
      opening_hours: "08:00",
      description: "quidem quis quia",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=48.33317711631233",
      viewCounts: null,
      createdAt: "2019-11-20T06:25:42.929Z",
      updatedAt: "2019-11-20T06:25:42.929Z",
      CategoryId: null,
      Category: null,
      isFavorited: false,
      isLiked: false
    },
    {
      id: 36,
      name: "Kale Nicolas",
      tel: "1-129-966-2808",
      address: "54065 Austin Plains",
      opening_hours: "08:00",
      description: "Est et id saepe tenetur et veritatis et. Qui simil",
      image:
        "https://loremflickr.com/320/240/restaurant,food/?random=11.056442083543061",
      viewCounts: null,
      createdAt: "2019-11-20T06:25:42.929Z",
      updatedAt: "2019-11-20T06:25:42.929Z",
      CategoryId: null,
      Category: null,
      isFavorited: false,
      isLiked: false
    }
  ],
  categories: [
    {
      id: 6,
      name: "美式料理",
      createdAt: "2019-11-20T06:25:42.917Z",
      updatedAt: "2019-11-20T06:25:42.917Z"
    },
    {
      id: 7,
      name: "複合式料理",
      createdAt: "2019-11-20T06:25:42.917Z",
      updatedAt: "2019-11-20T06:25:42.917Z"
    }
  ],
  categoryId: null,
  page: 1,
  totalPage: [1, 2, 3, 4, 5, 6],
  prev: 1,
  next: 2
};
export default {
  components: {
    Navtab,
    RestaurantCard,
    RestaurantsNavPills,
    RestaurantsPagination
  },
  data() {
    return {
      categories: [],
      categoryId: -1,
      currentPage: 1,
      restaurants: [],
      totalPage: -1
    };
  },
  created() {
    this.fetchRestaurants();
  },
  methods: {
    fetchRestaurants() {
      this.categories = dummyData.categories;
      this.categoryId = dummyData.categoryId;
      this.currentPage = dummyData.page;
      this.restaurants = dummyData.restaurants;
      this.totalPage = dummyData.totalPage.length;
    }
  }
};
</script>