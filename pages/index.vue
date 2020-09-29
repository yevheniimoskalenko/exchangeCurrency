<template>
  <div class="home">
    <el-form :model="controller" ref="form">
      <div class="give">
        1
      </div>
      <div class="get">
        2
      </div>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      controller: {
        give: null
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>
