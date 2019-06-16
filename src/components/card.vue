<template>
  <div class="card card_shadow text-center">
    <div class="card__content">
      <a class="card__avatar avatar">
        <img class="avatar__img" :src="avatar" alt="avatar">
      </a>
      <h4 class="card__name">{{name}}</h4>
      <div class="card__job">{{job}}</div>
      <p class="card__text">{{text}}</p>
      <div class="card__social">
        <a class="icon bd-twitter" href="javascript:void(0)"></a>
        <a class="icon bd-facebook" href="javascript:void(0)"></a>
        <a class="icon bd-dribbble" href="javascript:void(0)"></a>
        <a class="icon bd-github" href="javascript:void(0)"></a>
      </div>
      <button class="btn btn-primary waves-effect waves-classic">Follow</button>
    </div>
    <div class="card__footer">
      <div class="card__stat">
        <strong class="card__stat-count">{{follower}}</strong>
        <span>Follower</span>
      </div>
      <div class="card__stat">
        <strong class="card__stat-count">{{following}}</strong>
        <span>Following</span>
      </div>
      <div class="card__stat">
        <strong class="card__stat-count">{{tweets}}</strong>
        <span>Tweets</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    avatar: String,
    name: String,
    job: String,
    text: String,
    follower: Number,
    following: Number,
    tweets: Number
  }
};
</script>

<style scoped lang="scss">
.card {
  &_shadow {
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  }
  &__content {
    padding: 40px 15px;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  &__avatar {
    width: 130px;
    margin-bottom: 10px;
  }
  &__name {
    margin-bottom: 10px;
    color: #212121;
  }
  &__job {
    margin-bottom: 20px;
    color: #9e9e9e;
  }
  &__social {
    margin: 25px 0;
  }
  &__footer {
    display: flex;
		justify-content: space-around;
    padding: 10px;
    background-color: #f6f9fd;
    border-top: none;
    color: #9e9e9e;
  }
  &__stat-count {
    display: block;
    margin-bottom: 3px;
    font-size: 20px;
    font-weight: 500;
    color: #616161;
  }
}
</style>
