<script>
import Category from './components/Category';
import Tasklist from './components/Tasklist';
import Taskform from './components/Taskform';

export default {
  data() {
    return {
      dataList: {
        0: {
          categoryId: 0,
          categoryName: '默认分类',
          tasklists: [
            {
              taskId: 0,
              taskName: '任务1',
              deadline: new Date('2016-8-15'),
              priority: 0,
              hasCompleted: false,
              addTime: new Date('2016-8-10'),
            },
            {
              taskId: 1,
              taskName: '任务2',
              deadline: new Date('2016-8-11'),
              priority: 1,
              hasCompleted: true,
              addTime: new Date('2016-8-10'),
            },
            {
              taskId: 2,
              taskName: '任务3',
              deadline: new Date('2016-8-12'),
              priority: 2,
              hasCompleted: true,
              addTime: new Date('2016-8-10'),
            },
            {
              taskId: 3,
              taskName: '任务4',
              deadline: new Date('2016-8-13'),
              priority: 3,
              hasCompleted: false,
              addTime: new Date('2016-8-10'),
            },
          ],
        },
        1: {
          categoryId: 1,
          categoryName: '学习',
          tasklists: [
            {
              taskId: 0,
              taskName: '任务1',
              deadline: new Date('2016-8-11'),
              priority: 0,
              hasCompleted: false,
              addTime: new Date('2016-8-10'),
            },
          ],
        },
      },
      taskData: {},
    };
  },
  components: {
    Category,
    Tasklist,
    Taskform,
  },
  methods: {
    handleCate(id) {
      this.taskData = this.dataList[id];
    },
  },
};
</script>

<template>
  <div class="gtd-head">GTD Tools</div>
  <div class="gtd-body">
    <category :data-list="dataList"  v-on:clickcate="handleCate"></category>
    <tasklist :task-list="taskData"></tasklist>
    <taskform></taskform>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  height: 100%;
  font-family: Source Sans Pro, Helvetica, sans-serif;
}

body {
  height: 100%;
  display: flex;
  flex-flow: column;
}
.gtd-head {
  height: 50px;
  font-size: 24px;
  color: #4e4e4e;
  background: #ddd;
  line-height: 50px;
  padding-left: 25px;
}
.gtd-body {
  display: flex;
  flex-grow: 1;
}
</style>
