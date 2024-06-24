<template>
  <div class="UserInfo">
    <div v-if="!!error" class="empty">
      <span class="message">
          Ошибка: {{ error }}
        </span>
    </div>

    <div 
      v-else-if="!!userData" 
      class="content"
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
          {{ userData.name }}
        </div>

        <div class="contacts">
          <div class="contact">
            <b>email:</b>&nbsp; {{ userData.email }}
          </div>

          <div class="contact">
            <b>phone:</b>&nbsp; {{ userData.phone }}
          </div>
        </div>

        <div class="about">
          <div class="text">
            <b>О себе:</b>
          </div>

          <div class="description">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, 
            sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
            Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip 
            ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse 
            cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, 
            sunt in culpa qui officia deserunt mollit anim id est laborum.
          </div>
        </div>
      </div>
    </div>

    <div v-else class="empty">
      <span class="message">
        Выберите сотрудника, чтобы посмотреть его профиль
      </span>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: 'UserInfo',

  computed: {
    ...mapGetters({
      userData: 'getActiveUser',
      error: 'getError',
    }),
  },
}
</script>

<style lang="scss" scoped>
.UserInfo {
  width: 100%;
}

.content {
  display: flex;
  gap: 61px;
  padding: 30px 30px 30px 21px;
}

.photo {
  display: flex;
  flex-grow: 1;
  border: 1px solid #E0E0E0;
  width: 100%;
  height: 100%;
  min-width: 424px;
  max-height: 286px;
  user-select: none;
}

.img {
  width: 100%;
}

.info {
  text-align: left;
  color: #000000;
}

.name {
  font-size: 16px;
  font-weight: 600;
  line-height: 22.4px;
  margin-bottom: 10px;
}

.contacts {
  margin-bottom: 20px;
}

.contact {
  font-size: 14px;
  font-weight: 400;
  line-height: 19.6px;

  &:not(:last-child) {
    margin-bottom: 10px;
  }

  b {
    font-weight: 600;
  }
}

.text {
  margin-bottom: 25px;
}

.description {
  font-size: 14px;
  font-weight: 400;
  line-height: 17.07px;
  color: #76787D;
}

.empty {
  display: flex;
  width: 100%;
  height: 100%;
  min-width: 100%;
  user-select: none;
}

.message {
  margin: auto;
  font-size: 14px;
  font-weight: 400;
  line-height: 17.07px;
  text-align: left;
  color: #76787D;
}

@media (max-width: 1180px) {
  .content {
    flex-wrap: wrap;
  }

  .photo {
    min-width: auto;
    max-height: auto;
  }
}
</style>
