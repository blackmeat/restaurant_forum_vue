<template>
  <div>
    <div>
      <blockquote class="blockquote mb-0">
        <button
          v-if="currentUser.isAdmin"
          type="button"
          class="btn btn-danger float-right"
          @click.stop.prevent="handleDeleteButtonClick(comment.id)"
        >Delete</button>
        <h3>
          <a href="#">{{comment.User.name}}</a>
        </h3>
        <p>{{comment.text}}</p>
        <footer class="blockquote-footer">{{comment.createdAt|fromNow}}</footer>
      </blockquote>
      <hr />
    </div>
  </div>
</template>

<script>
import { fromNowFilter } from "../utils/mixins";
const dummyUser = {
  currentUser: {
    id: 1,
    name: "管理者",
    email: "root@example.com",
    image: "https://i.pravatar.cc/300",
    isAdmin: true
  },
  isAuthenticated: true
};
export default {
  mixins: [fromNowFilter],
  props: {
    restaurantComments: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      currentUser: dummyUser.currentUser,
      comment: this.restaurantComments
    };
  },
  methods: {
    handleDeleteButtonClick(commentId) {
      console.log("handleDeleteButtonClick", commentId);
      // TODO: 請求 API 伺服器刪除 id 為 commentId 的評論
      // 觸發父層事件 - $emit( '事件名稱' , 傳遞的資料 )
      this.$emit("after-delete-comment", commentId);
    }
  }
};
</script>