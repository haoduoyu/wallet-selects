<!--
 * @Author: your name
 * @Date: 2021-02-15 16:22:37
 * @LastEditTime: 2021-02-18 14:37:58
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: /swap-select/src/components/ChosseWallet.vue
-->
<template>
  <div class="choose-wallet">
    <div class="mask">
      <div class="wrap">
        <div class="choose-title">
          Choose a wallet
        </div>
        <div class="choose-main">
          <ul>
            <li v-for="(item, index) in walletArr" :key="index" @click="goWallet(item)" :class="{ select: item.wallet_name === walletName }">
              <div class="wallet-info">
                <div class="wallet-logo"></div>
                <div class="wallet-name">{{item.wallet_name}}</div>
              </div>
              <div class="arrow">></div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { initContract } from '../utils/utils.js'
export default {
  data () {
    return {
      walletArr: [],
      walletName: ''
    }
  },
  methods: {
    async getWallet () {
      const walletArr = await window.contract.get_wallets({ from_index: 0, limit: 100 })
      console.log(walletArr)
      this.walletArr = walletArr
    },
    goWallet (item) {
      window.localStorage.setItem('walletName', item.wallet_name)
      window.location.href = (item.wallet_url + window.location.search)
    },
    getWalletName () {
      const name = window.localStorage.getItem('walletName')
      this.walletName = name
    }
  },
  created () {
    const that = this
    initContract()
      .then(() => {
        that.getWallet()
        that.getWalletName()
      })
  }
}
</script>

<style lang="less" scoped>
  .mask {
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .6);
    position: absolute;
    left: 0;
    top: 0;
    z-index: 999;
    display: flex;
    justify-content: center;
    align-items: center;
    .wrap {
      width: 500px;
      /* height: 300px; */
      background-color: #fff;
      border-radius: 10px;
      padding: 40px 20px 20px;
      .choose-title {
        padding-bottom: 20px;
        font-size: 20px;
      }
      .choose-main {
        ul {
          li {
            width: 100%;
            padding: 10px;
            display: flex;
            height: 80px;
            border: 1px solid #000;
            border-radius: 10px;
            margin-bottom: 10px;
            cursor: pointer;
            align-items: center;
            justify-content: space-between;
          }
          .select {
            border-color: rgb(214, 62, 62);
          }
        }
      }
    }
  }
</style>
