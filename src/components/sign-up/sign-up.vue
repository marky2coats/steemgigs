<template>
  <el-dialog class="sign-up-modal" :visible.sync="show" width="65%" @closed="sendBasicEvent('closeSignUp')">
    <template slot="title"><h3>Get your Steem Account today</h3>
</template>
    <p>Signing up to Steem unlocks your chance to use hundreds of awesome Steem apps as well as SteemGigs.</p>
    <el-row :gutter="25">
            <el-col class="sign-up-item" v-for="(item, index) in signUpOptions" :key="index" :xs="24" :sm="24" :md="12" :lg="12" :xl="12">
              <img :src="item.image" alt="Sign Up Image">
              <p>{{ item.text }}</p>
              <el-button :disabled="item.disabled" :type="item.buttonType" :class="item.buttonType" @click="handleNext(item.type)"> {{ item.buttonText }}</el-button>
              <p>{{ item.waitTime }}</p>
            </el-col>
    </el-row>
  </el-dialog>
</template>

<script>
import modal from '@/mixins/modal.js'
export default {
  name: 'sign-up',
  mixins: [modal],
  props: {
    show: Boolean
  },
  data () {
    return {
      signUpOptions: [{
        image: '/static/img/sign-up/clock.svg',
        text: 'Sign up via Steemit.com for free, but takes longer to verify you account',
        waitTime: '3 - 10 Day Waiting Time ',
        buttonText: 'Sign Up For Free',
        buttonType: 'secondary',
        type: 1,
        disabled: false
      },
      {
        image: '/static/img/sign-up/finish.svg',
        text: 'Sign up directly from SteemGigs, costs $2, but you get instant access.',
        waitTime: 'Instant Access',
        buttonText: 'Get Instant Access (Coming Soon)',
        buttonType: 'primary',
        type: 2,
        disabled: true
      }
      ]
    }
  },
  methods: {
    handleNext (type) {
      switch (type) {
        case 1:
          window.open('https://signup.steemit.com/', '_blank')
          break
        case 2:
          alert('Sign ups coming soon')
          break
      }
    }
  }
}
</script>

<style lang="scss">
  .sign-up-modal {
    text-align: center;
    .el-dialog {
      padding: 30px;
        .sign-up-item {
          padding: 10px;
        }
        img {
          width: 100%;
          max-width: 200px;
          height: 145px;
        }
      }
    }
</style>
