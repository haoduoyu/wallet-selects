<!--
 * @Author: your name
 * @Date: 2021-02-15 16:07:41
 * @LastEditTime: 2021-02-15 16:31:28
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: /swap-select/src/views/Index.vue
-->
<template>
  <div class="index">
    <choose-wallet></choose-wallet>
  </div>
</template>

<script>
import ChooseWallet from '@/components/ChooseWallet.vue'
export default {
  name: 'index',
  components: {
    ChooseWallet
  }
}
</script>

<style lang="less" scoped></style>
