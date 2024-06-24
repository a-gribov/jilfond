<template>
  <div 
    class="UserCard" 
    :class="{'_active': isActive}" 
    @click="onCardClick(userData.id)"
  >
    <div class="photo">
      <img 
        class="img" 
        :alt="userData.username" 
        src="@/assets/img/photo.svg"
      >
    </div>

    <div class="info">
      <div class="name">
        {{ userData.username }}
      </div>

      <div class="email">
        {{ userData.email }}
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  name: 'UserCard',

  props: {
    userData: Object
  },

  computed: {
    ...mapGetters({
      activeUserId: 'getActiveUserId',
    }),

    isActive() {
      return this.activeUserId === this.userData.id
    },
  },

  methods: {
    ...mapActions({
      setActiveUserId: 'setActiveUserId',
    }),

    onCardClick(id) {
      this.setActiveUserId(id)
    }
  },
}
</script>

<style lang="scss" scoped>
.UserCard {
  display: flex;
  border-radius: 10px;
  box-shadow: 0px 0px 10px 0px #0000001A;
  overflow: hidden;
  user-select: none;

  &._active .info {
    background-color: #E0E0E0;
  }

  &:not(._active) {
    cursor: pointer;
    
    &:hover .info {
      background-color: #efeded;
    }
  }
}

.photo {
  border-right: 1px solid #E0E0E0;
  width: 70px;
  height: 70px;
}

.img {
  object-fit: contain;
  object-position: center;
}

.info {
  width: 100%;
  padding: 15px;
  font-size: 14px;
  line-height: 17.07px;
  text-align: left;
  overflow: hidden;
  transition: background-color .3s ease;
}

.name,
.email {
  text-overflow: ellipsis;
  max-width: 100%;
  overflow: hidden;
}

.name {
  font-weight: 600;
  margin-bottom: 5px;
  color: #333333;
}

.email {
  font-weight: 400;
  color: #76787D;
}
</style>
