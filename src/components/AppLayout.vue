<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import { Back } from '@element-plus/icons-vue'
import { ROUTES_PATHS } from '@/constants'



const props = defineProps({
    imgUrl: {
        type: String,
        required: true,
    },
    backFunc: {
      type: Function,
    },
    isBackButtonVisible: {
      type: Boolean,
      default: true,
    }
})

const route = useRoute();
const router = useRouter();

const routName = computed(() => route.name);

function goForCoctailRandom() {
  router.push(ROUTES_PATHS.COCKTAIL_RANDDOM)

  if(routName.value === ROUTES_PATHS.COCKTAIL_RANDDOM) {
    router.go()
  }
}

function goBack() {
  props.backFunc ? props.backFunc() : router.go(-1);
}
</script>

<template>
  <div class="root">
    <div :style="`background-image: url(${imgUrl})`" class="img">

    </div>
    <div class="main">
      <div class="btns">
        <el-button 
          v-if="isBackButtonVisible"
          type="primary" 
          :icon="Back" 
          class="back" 
          circle 
          @click="goBack"
        />
        <el-button class="btn" @click="goForCoctailRandom">Get random coctail</el-button>
      </div>
        
        <slot></slot>
    </div>
  </div>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main.sass'
.root
 display: flex
 height: 100vh
 background: $background

.img
  width: 50%
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: cover

.main
    width: 50%
    margin: 32px 40px
    position: relative

.btn
  position: absolute
  top: 32px
  right: 40px
  font-size: 16px
  font-family: 'Raleway', 'Arial', sans-seref
  background: $accent
  border-color: $accent
  color: $text

  &:hover,
  &:active
    background: darken($accent, 10%)
    border-color: darken($accent, 10%)

.btns
  display: flex
  justify-content: space-between
  align-items: center

.back
  background-color:  transparent
  border-color: #fff
  &:hover
    border-color: $accent
</style>
