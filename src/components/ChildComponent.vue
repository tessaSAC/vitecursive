<script>
import { ref, reactive } from 'vue'

const count = ref(0)

export default {
  name: 'ChildComponent',

setup() {
      const count = ref(0)
      return {
        count,

        nested: {
          count
        }
      }
    },

  props: {
    parentNumber: Number,
    numChildren: Number,
  },

  data: () => ({
    myStyle: {
      background: 'linear-gradient(160deg, rgba(228,228,228,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      border: '1px solid',
      borderRadius: '4px',
    },

    bgColorsPossible: [
      'linear-gradient(336deg, rgba(104,99,185,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(99,185,150,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(214,161,220,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(255,208,131,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(255,244,131,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(255,140,131,0.5) 0%, rgba(216,248,255,0.5) 100%)',
      'linear-gradient(336deg, rgba(131,153,255,0.5) 0%, rgba(216,248,255,0.5) 100%)',
    ]
  }),

  computed: {
    myNumber() {
      return this.parentNumber + 1
    },

    numChildrenLeft() {
      return this.numChildren - 1
    },
  },

  methods: {
    alertButtonClicked() {
      console.warn('BUTTON CLICKED!')
      console.log(count.value)
      count.value++
    },

    getBgColor() {
      const whichColor = Math.floor(Math.random() * this.bgColorsPossible.length)

      this.myStyle.background = this.bgColorsPossible[whichColor]
    },
  },

  created() {
    this.getBgColor()
    console.log('created')
  },

  mounted() {
    console.log('mounted')
  }
}
</script>

<template>
  <el-card :body-style="myStyle">
    <el-row align="middle" justify="space-around">
      <el-col :span="6">
        <h2>Child no. {{ count }}</h2>
      </el-col>
      <el-col :span="8">
        <el-button plain round type="warning" @click="alertButtonClicked">Change color</el-button>
      </el-col>
    </el-row>

    <ChildComponent v-if="numChildrenLeft" :parentNumber="myNumber" :numChildren="numChildrenLeft" />
  </el-card>
</template>

<style scoped>
.el-row {
  padding: 0.5rem 0 1rem 0;
}

h2 {
  font-size: 1.2rem;
}
</style>
