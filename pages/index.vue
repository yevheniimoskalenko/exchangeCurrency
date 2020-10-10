<template>
  <div class="home">
    <el-form :model="controller" ref="form">
      <div class="give">
        <h2>Віддаємо</h2>
        <el-form-item label="Що ви хочите обміняти!">
          <el-select placeholder="Виберіти" v-model="controller.firstCurrency">
            <el-option label="Privat24" value="privat24" />
          </el-select>
        </el-form-item>
        <el-form-item label="Із рахунку">
          <el-input
            v-model="controller.giveNumber"
            v-mask="'#### #### #### ####'"
            placeholder="4321 1234 5678 9012"
          />
        </el-form-item>
        <el-form-item label="Сумма">
          <el-input
            v-model="controller.giveAmount"
            @keypress.native="giveSum($event)"
          />
        </el-form-item>
      </div>
      <div class="get">
        <h2>Отримуємо</h2>
        <el-form-item label="Що ви хочите отримати!">
          <el-select placeholder="Виберіти" v-model="controller.secondCurrency">
            <el-option label="Payeer" value="payeer" />
          </el-select>
        </el-form-item>
        <el-form-item label="На рахунку">
          <el-input
            v-model="controller.getNumber"
            placeholder="P"
            v-mask="'P ########'"
          />
        </el-form-item>
        <el-form-item label="Отримуємо сумму">
          <el-input v-model="controller.getAmount" disabled />
        </el-form-item>
      </div>
      <div class="rec">
        <h2>Реквізити</h2>
        <el-form-item label="ПІП">
          <el-input v-model="controller.fullName"></el-input>
        </el-form-item>
        <el-form-item label="Номер телефону">
          <el-input
            v-model="controller.phoneNumber"
            placeholder="(066)465-70-82"
            v-mask="'(0##)###-##-##'"
          />
        </el-form-item>
      </div>
      <el-button round type="primary" @click="createPay"
        >Створити платиж</el-button
      >
    </el-form>
  </div>
</template>

<script>
import procent from '@/components/mixins/procent'
import cours from '@/components/mixins/course'
export default {
  mixins: [cours],
  data() {
    return {
      loading: false,
      controller: {
        giveNumber: '',
        giveAmount: 0,
        getNumber: '',
        getAmount: 0,
        fullName: null,
        phoneNumber: null,
        firstCurrency: null,
        secondCurrency: null,
      },
    }
  },
  methods: {
    createPay() {
      this.$refs.form.validate(async (valid) => {
        try {
          const form = {
            card: controller.giveNumber,
            giveAmount: controller.giveAmount,
            getNumber: controller.getNumber,
            getAmount: controller.getAmount,
            fullName: controller.fullName,
            phoneNumber: controller.phoneNumber,
            firstCurrency: controller.firstCurrency,
            secondCurrency: controller.secondCurrency,
          }
          await this.$store.dispatch('payAmount', form)
        } catch (e) {
          throw new Error(e)
        }
      })
    },
    giveSum() {
      this.$refs.form.validate(async (valid) => {
        if (valid) {
          try {
            let sum = await this.cours()
            let sale = sum[1].sale

            let total = +this.controller.giveAmount / sale
            this.controller.getAmount = total.toFixed(2)
          } catch (e) {
            throw new Error(e)
          }
        }
      })
    },
  },
}
</script>

<style lang="scss" scoped></style>
