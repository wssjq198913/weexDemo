<template>
  <div class="wrapper">
    <wxc-minibar title="标题"
                   background-color="#009ff0"
                   text-color="#FFFFFF"
                   right-text="更多"></wxc-minibar>
    <image :src="logo" class="logo" />
    <text class="greeting">The environment is ready!</text>
    <HelloWorld/>
    <div class="group">
      <text class="button" @click="pickTime">Pick Tim1e</text>
      <text class="button" @click="jump">Ju1mp</text>
    </div>
    <WxcButton text="Open Popup"
                  @wxcButtonClicked="buttonClicked">
    </WxcButton>
    <wxc-popup width="500"
                pos="left"
                :show="isShow"
                @wxcPopupOverlayClicked="overlayClicked">
    </wxc-popup>
    <text class='top-text' @click='chooseShop'>选择门店</text>
  </div>
</template>

<script>
import { WxcButton, WxcPopup, WxcMinibar } from 'weex-ui';
import HelloWorld from './components/HelloWorld';

const picker = weex.requireModule('picker');
const navigator = weex.requireModule('navigator');
const modal = weex.requireModule('modal');


export default {
  name: 'App',
  components: {
    HelloWorld,
    WxcButton,
    WxcPopup,
    WxcMinibar,
  },
  data: () => ({
    logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png',
    isShow: false,
  }),
  methods: {
    buttonClicked() {
      this.isShow = true;
    },
    overlayClicked() {
      this.isShow = false;
    },
    pickTime() {
      picker.pickTime({
        value: this.value,
      }, (event) => {
        if (event.result === 'success') {
          this.value = event.data;
        }
      });
    },
    chooseShop() {
      picker.pick({
        items: [1, 2, 3, 4],
        height: '500px',
      }, () => {
      });
    },
    jump() {
      // console.log('will jump');
      navigator.push({
        url: 'https://www.baidu.com',
        animated: 'true',
      }, (event) => {
        modal.toast({ message: `callback: ${event}` });
      });
    },
  },
};
</script>

<style scoped>
  .wrapper {
    /* justify-content: center;
    align-items: center; */
  }
  .logo {
    width: 424px;
    height: 200px;
  }
  .greeting {
    text-align: center;
    margin-top: 70px;
    font-size: 50px;
    color: #41B883;
  }
  .message {
    margin: 30px;
    font-size: 32px;
    color: #727272;
  }
</style>
