<template>
  <div id="pic">
    <div>
      {{ jokes.tip }}
    </div>
    <joke v-for="item in jokes.data" :key="item.display_time" :joke="item.group" :comments="item.comments"></joke>
  </div>
</template>

<style scoped>
#pic{
  background: #eee;
}
</style>

<script>
import joke from '@/commons/joke'
export default {
  props: ['refresh'],
  mounted () {
    this.getInfo()
  },
  data () {
    return {
      jokes: ''
    }
  },
  components: {
    joke
  },
  watch: {
    'refresh': 'getInfo'
  },
  methods: {
    getInfo () {
      document.body.scrollTop = document.documentElement.scrollTop = 0
      this.$ajax({
        methods: 'get',
        baseURL: '/lf',
        url: 'neihan/stream/mix/v1/?content_type=-103'
      }).then((res) => {
        console.log('图片')
        console.log(res.data.data)
        this.jokes = res.data.data
      })
    }
  }
}
</script>