<template>
  <div class="wrapper">
    <div class="contaiber-fluid content">
      <div class="row">
        <div class="col-lg-3">
          <card
            avatar="img/5.webp"
            name="Terrance arnold"
            job="Art director"
            text="Hi! I'm Adrian the Senior UI Designer at AmazingSurge. We hope you enjoy the design and quality of Social."
            follower="260"
            following="180"
            tweets="2000"
          ></card>
        </div>
        <div class="col-lg-9">
          <panel></panel>
        </div>
      </div>
    </div>
    <div class="footer">футер</div>
  </div>
</template>

<script>
import card from "./components/card.vue";
import panel from "./components/panel.vue";
import post from "./components/post.vue";

export { post };

export default {
  name: "app",
  // data: {},
  data() {
    return {
      users: [
        { id: "0", name: "Terrance arnold", online: "", avatar: "img/5.webp" },
        { id: "1", name: "Owen Hunt", online: "", avatar: "img/4.webp" },
        { id: "2", name: "Ida Fleming", online: "", avatar: "img/2.jpg" },
        {
          id: "3",
          name: "Julius",
          online: "10 minutes ago",
          avatar: "img/3.jpg"
        }
      ]
    };
  },
  components: {
    card,
    panel,
    post
  }
};
</script>

<style lang="scss">
html,
body {
  height: 100%;
}
.wrapper {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.content {
  flex: 1 0 auto;
  min-height: 100%;
  background: #f1f4f5;
  padding: 30px;
}
.footer {
  flex: 0 0 auto;
}
.avatar {
  display: block;
  border-radius: 70%;
  overflow: hidden;
  &__img {
    width: 100%;
  }
}
.waves-effect {
  position: relative;
  z-index: 1;
  display: inline-block;
  overflow: hidden;
  cursor: pointer;
  user-select: none;
}
</style>
