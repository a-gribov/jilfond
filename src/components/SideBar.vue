<template>
  <div class="SideBar">
    <div class="search">
      <h2>Поиск сотрудников</h2>

      <input 
        type="text" 
        class="input" 
        placeholder="Введите Id или имя"
        v-model="searchText" 
      >
    </div>

    <div class="list">
      <h2>Результаты</h2>

      <template v-if="lazyList.length">
        <UserCard
          v-for="userData in lazyList"
          :key="userData.id"
          :user-data="userData"
          class="item"
        />
      </template>

      <InfiniteLoading
        v-if="isNeedScroll" 
        @infinite="infiniteHandler" 
      />

      <div 
        v-if="!lazyList.length && !isNeedScroll" 
        class="empty"
      >
        <span v-if="searchText">ничего не найдено</span>

        <span v-else>начните поиск</span>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

import UserCard from '@/components/UserCard.vue'
import InfiniteLoading from 'vue-infinite-loading';

export default {
  name: 'SideBar',

  components: {
    UserCard,
    InfiniteLoading
  },

  data() {
    return {
      searchText: '',
      lastSearchArr: [],
      counter: 1,
    }
  },

  computed: {
    ...mapGetters({
      userList: 'getUsersList',
      isLoading: 'getIsLoading',
    }),

    searchArr () {
      return (this.searchText.trim()).split(',').map(item => item.trim())
    },

    clearedSearchArr () {
      return [...new Set(this.searchArr.filter(item => item !== ''))]
    },

    lazyList () {
      return this.userList.slice(0, (2 * this.counter))
    },

    isUsers () {
      return !!this.userList.length
    },

    isNeedScroll () {
      return this.userList.length !== this.lazyList.length || this.isLoading
    }
  },

  watch: {
    clearedSearchArr() {
      const sortedSearchArr = this.clearedSearchArr.sort()

      if (sortedSearchArr.toString() === this.lastSearchArr){ 
        return
      }

      this.lastSearchArr = sortedSearchArr.toString()
      this.loadUsers(this.searchArr)
    }
  },
  
  methods: {
    ...mapActions({
      loadUsers: 'loadUsers',
    }),

    infiniteHandler($state) {
      setTimeout(() => {
        if (this.userList.length !== this.lazyList.length) {
          this.counter++
        }
        
        $state.loaded();
      }, 500);
    },
  },
}
</script>

<style lang="scss" scoped>
.SideBar {
  padding: 27px 31px 20px 20px;
  overflow: auto;

  h2 {
    margin: 0;
    font-size: 16px;
    font-weight: 600;
    line-height: 22.4px;
    text-align: left;
    color: #333333;
    user-select: none;
  }
}

.search {
  margin-bottom: 29px;

  h2 {
    margin-bottom: 14px;
  }
}

.input {
  width: 100%;
  box-sizing: border-box;
  padding: 16px;
  border: 1.5px solid #E9ECEF;
  color: #76787D;
  border-radius: 8px;
  font-family: "Montserrat", sans-serif;
  font-size: 14px;
  font-weight: 400;
  line-height: 17.07px;
  text-align: left;
}

.list {
  h2 {
    margin-bottom: 18px;
  }
}

.item {
  margin-bottom: 18px;
}

.empty {
  font-size: 14px;
  font-weight: 400;
  line-height: 17.07px;
  text-align: left;
  color: #76787D;
}
</style>
