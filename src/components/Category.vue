<script>
export default {
  props: {
    dataList: Object,
  },
  data () {
    return {
      categoryData: {},
      showCate: false,
      activeItem: '',
    };
  },
  filters: {
    notCompleteCount(value) {
      return value.filter(v => {
        return !v.hasCompleted;
      }).length;
    },
    notCompleteAllCount(value) {
      let array = [];
      for (let key in value) {
        array = array.concat(value[key].tasklists);
      }
      return array;
    },
  },
  methods: {
    clickCate(id) {
      this.activeItem = id;
      this.$dispatch('clickcate', typeof id === 'string' ? id : 'all');
    },
    deleteCate(id, name) {
      if (confirm(`delete the ${name}`)) {
        console.log('deleted');
      }
    },
  },
};
</script>

<template>
  <div class="category">
    <div @click="clickCate">所有任务({{dataList | notCompleteAllCount | notCompleteCount}})</div>
    <div>
      <p @click="showCate = !showCate">分类列表</p>
      <ul v-show="showCate">
        <li v-for="cate in dataList" @click="clickCate($key)" :class="{'blue': activeItem === $key}">
          {{cate.categoryName}}({{cate.tasklists | notCompleteCount}})
          <span @click.stop="deleteCate($key, cate.categoryName)">X</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
  .category {
    background: #f2f2f2;
    color: #868686;
    line-height: 2;
    padding: 10px;
    width: 200px;
    cursor: pointer;
  }
  ul {
    padding-left: 20px;
    list-style: none;
  }
  
  li > span {
    display: none;
    width: 30px;
    float: right;
    text-align: center;
  }
  li:hover > span {
    display: block;
  }
  .blue {
    color: #0089dc;
  }
</style>
