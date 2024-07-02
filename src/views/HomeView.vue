<template>
  <div class="home">
    <list ref="list" msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import list from '@/components/list.vue'

export default {
  name: 'HomeView',
  components: {
    list
  },
  data() {
    return {
      offset: 0
    }
  },
  beforeRouteLeave(to, from, next) {
    this.offset = this.$refs.list.$refs.virtListRef.getOffset();
    next()
  },
  activated() {
     if(this.offset > 0) {
      this.$refs.list.$refs.virtListRef.scrollToOffset(this.offset);
     }
  }
}
</script>
