<template>
  <div class="home">
    <about height="300" width="604" :model="data" :header="header" :hebing-info="hebing" :n="count"></about>
  </div>
</template>

<script>
import about from './About'
import data from './data.json'
export default {
  name: 'home',
  data() {
    return {
      count:1,
      hebing:{
        hang:'2',
        aaa:['1','2','3']
      },
      header: [],
      data: [],
    }
  },
  mounted(){
    this.data = data.data
    this.header = data.header
  },
  components: {
    about
  }
}
</script>
