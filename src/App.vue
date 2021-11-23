<script>
import ChildComponent from './components/ChildComponent.vue'

export default {
  name: 'App',
  components: {
    ChildComponent
  },

  data: () => ({
    numChildren: 0,
  }),

  methods: {
    addChild() {
      ++this.numChildren
    }
  },

  created() {
    console.log('App created')
  },

  mounted() {
    console.log('App mounted')
  }
}
</script>

<template>
  <el-container>
    <el-header height="2.5rem">
      <el-row justify="space-between" align="middle">
        <el-col :span="3">
          <h1>Main app</h1>
        </el-col>
        <el-col :span="3" class="numChildren">Child count: {{ numChildren }}</el-col>
        <el-col :span="3">
          <el-button plain round type="success" @click="addChild">Add child</el-button>
        </el-col>
      </el-row>
    </el-header>

    <el-main>
      <ChildComponent v-if="numChildren" :numChildren="numChildren" :parentNumber="0" />
    </el-main>
  </el-container>
</template>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#app {
  text-align: center;
  color: #2c3e50;
}

.el-container {
  padding: 2.5rem;
}

.el-header {
  padding: 0;
}

.el-main {
  padding: 1rem;
}
</style>
