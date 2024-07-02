<template>
  <div class="hello-vue-vrt-list">
    <h1>时间戳：{{ Date.now() }}</h1>
    <VirtList
        ref="virtListRef"
        :minSize="40"
        :list="list"
        itemKey="id"
        :buffer="2"
        @toBottom="toBottom"
        stickyHeaderStyle="text-align: center; height: 40px; background: #42b983;"
        headerStyle="text-align: center; height: 80px; background: cyan"
        footerStyle="text-align: center; height: 80px; background: cyan"
        stickyFooterStyle="text-align: center; height: 40px; background: #42b983;"
      >
        <template #default="{ itemData, index }">
          <itemDemo :itemData="itemData" :index="index" />
        </template>
        <template #stickyHeader>
          <div>悬浮header</div>
        </template>
        <template #header>
          <div>header</div>
        </template>
        <template #footer>
          <div>footer</div>
        </template>
        <template #stickyFooter>
          <div>悬浮footer</div>
        </template>
      </VirtList>
  </div>
</template>

<script>
import { VirtList } from 'vue-virt-list';
import { faker } from '@faker-js/faker';
import itemDemo from "./itemDemo.vue";
export default {
  name: 'HelloWorld',
  components: { VirtList, itemDemo },
  data() {
    return {
      visible: true,
      list: [],
      virtListRef: null,
    }
  },
  mounted() {
    this.list = this.getList(20);
    console.log(this.list);
  },
  methods: {
    getList(length) {
      const newList = [];
      for (let i = 0; i < length; i++) {
        newList.push({
          index: i,
          id: faker.string.nanoid(),
          text: faker.lorem.sentences(),
        });
      }
      return newList;
    },
    toBottom() {
      if(this.list.length === 100) return false;
      const data = this.getList(20);
      this.list = this.list.concat(data);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello-vue-vrt-list {
  height: 600px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
