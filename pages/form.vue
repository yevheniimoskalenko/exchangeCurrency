<template>
  <div>
    <h1>Обмін валюти PrivatBank на Payeer</h1>

    <h2>Віддаємо</h2>
    <el-form :model="controls" ref="form">
      <el-form-item label="UAH">
        <el-input
          v-model.number="controls.amount"
          placeholder="Введите сумму"
          value="number"
          @keypress.native="genSum($event)"
        ></el-input>
      </el-form-item>
      <el-form-item label="RUB">
        <el-input
          v-model.number="controls.total"
          placeholder="Введите сумму"
          value="number"
          disabled
        ></el-input>
      </el-form-item>
      <el-form-item>
        <!-- <el-button @click="OnSubmit" type="primary" round :loading="loading"
          >Pay</el-button
        > -->
      </el-form-item>
    </el-form>
    <div v-html="form"></div>
  </div>
</template>

<script>
import cours from '@/components/mixins/course'
export default {
  head: {
    title: 'Пополнить'
  },
  mixins: [cours],
  components: {},
  data() {
    return {
      loading: false,
      form: null,
      controls: {
        amount: 0,
        total: 0
      }
    }
  },
  methods: {
    genSum() {
      this.$refs.form.validate(async (valid) => {
        if (valid) {
          try {
            console.log(await this.cours())
          } catch (e) {}
        }
      })
    },
    OnSubmit() {
      this.$refs.form.validate(async (valid) => {
        this.loading = true
        const formData = {
          amount: this.controls.amount
        }
        try {
          await this.$store.dispatch('payAmount', formData)
          this.form = this.$store.state.form
        } catch (e) {}
        this.loading = false
      })
    }
  }
}
</script>

<style></style>
