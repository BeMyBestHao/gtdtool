<script>
const STATUS = {
  all: '全部',
  complished: '已完成',
  notComplished: '未完成',
};
export default {
  props: {
    taskList: {
      type: Object,
    },
  },
  data () {
    return {
      status: STATUS,
      active: 'all',
      flagStyle: ['', '#80beeb', '#2178bb', '#bb5224'],
      activeItem: '',
    };
  },
  filters: {
    formatTime(value) {
      return `${value.getFullYear()}-${value.getMonth() + 1}-${value.getDate()}`;
    },
  },
  methods: {
    toggleStatus(key) {
      this.active = key;
    },
    clickItem(id) {
      this.activeItem = id;
    },
  }
};
</script>

<template>
  <div class="tasklist">
    <div class="task-header">
      <span v-for="item in status" @click="toggleStatus($key)" :class="{'active' : active === $key}">
        {{item}}
      </span>
    </div>
    <ul v-if="taskList.tasklists && taskList.tasklists.length">
      <li v-for="item in taskList.tasklists" @click="clickItem(item.taskId)" :class="{'active' : activeItem === item.taskId}">
        <p>
          <input type="checkbox" id="checkbox{{item.taskId}}" checked="{{item.hasCompleted}}" />
          <label for="checkbox{{item.taskId}}">{{item.taskName}}</label>
          <span class="flag" :style="{color: flagStyle[item.priority]}" v-if="item.priority">&#9873;</span>
        </p>
        <p v-if="item.deadline">{{item.deadline | formatTime}}</p>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .tasklist {
    width: 200px;
    border-left: 1px solid #ddd;
    border-right: 1px solid #ddd;
  }
  .task-header {
    padding: 10px;
    display: flex;
  }
  .task-header > span {
    padding: 5px;
    margin-right: 6px;
    font-size: 14px;
    border-radius: 5px;
  }
  ul {
    list-style: none;
    display: flex;
    flex-flow: column;
  }
  ul > li {
    height: 60px;
    padding: 6px;
  }
  li > p {
    line-height: 26px;
  }
  li > p:last-child {
    padding-left: 15px;
  }
  .active {
    background: #0089dc;
    color: #fff;
  }
  .flag {
    float: right;
    font-size: 24px;
  }
</style>
