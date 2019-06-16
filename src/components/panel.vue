<template>
  <div class="panel">
    <div class="tabs panel__inner">
      <ul class="tabs__links">
        <li class="tabs__link-wrap">
          <a class="tabs__link" @click="setActive(0)" :class="{'active': activeTab === 0}">
            Activities
            <span
              class="badge badge-pill badge-danger"
              v-if="newActivities"
            >{{newActivities}}</span>
          </a>
        </li>
        <li class="tabs__link-wrap">
          <a class="tabs__link" @click="setActive(1)" :class="{'active': activeTab === 1}">
            Profile
            <span class="badge badge-pill badge-danger" v-if="newProfile">{{newProfile}}</span>
          </a>
        </li>
        <li class="tabs__link-wrap">
          <a class="tabs__link" @click="setActive(2)" :class="{'active': activeTab === 2}">
            Messages
            <span class="badge badge-pill badge-danger" v-if="newMessages">{{newMessages}}</span>
          </a>
        </li>
      </ul>
      <div class="tabs__content">
        <div class="tabs__tab" v-if="activeTab === 0">
          <div class="post-list">
            <post></post>
          </div>
        </div>
        <div class="tabs__tab" v-if="activeTab === 1">2</div>
        <div class="tabs__tab" v-if="activeTab === 2">3</div>
      </div>
    </div>
  </div>
</template>
 
<script>

export default {
	name: 'panel',
  data() {
    return {
      activeTab: 0
    };
  },
  props: {
    newActivities: {
      default: 5,
      type: Number
    },
    newProfile: Number,
    newMessages: Number
  },
  methods: {
    setActive(num) {
      this.activeTab = num;
    }
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
    margin-bottom: -1px;
    display: flex;
  }
  &__link {
    cursor: pointer;
    color: #757575;
    transition: 0.25s;
    padding: 0.715rem 1.429rem;
    border-bottom: 2px solid transparent;
    &:hover {
      border-bottom-color: #bdbdbd;
    }
    &.active {
      color: #3f51b5;
      background-color: transparent;
      border-bottom: 2px solid #3f51b5;
    }
  }
}
</style>
