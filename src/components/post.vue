<template>
  <div class="post">
    <div class="post__inner">
      <div class="post__avatar-wrap">
        <img :src="avatar" alt class="avatar">
        aaaaaaaaaa
      </div>
    </div>
  </div>
</template>
 
<script>
export default {
  name: "post",
  props: {
    avatar: String,
    name: String,
    online: {
      default: "Online",
      type: String
    },
    imgSrc: [],
    text: String
  }
};
</script>

<style scoped lang="scss">
.panel {
  // margin-bottom: 2.143rem;
  background-color: #fff;
  border: 0 solid transparent;
  border-radius: 0.286rem;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  &__inner {
    padding: 30px;
  }
}

.tabs {
  &__links {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
    border-bottom: 1px solid #e0e0e0;
  }
  &__link-wrap {
    display: flex;
  }
  &__link {
    cursor: pointer;
    color: #757575;
    transition: 0.25s;
    padding: 0.715rem 1.429rem;
    border-bottom: 2px solid transparent;
    &.active {
      color: #3f51b5;
      background-color: transparent;
      border-bottom: 2px solid #3f51b5;
    }
  }
}
</style>
