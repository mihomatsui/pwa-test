<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { checkPWA } from '../../shared/pwa';
import { useRouter } from 'vue-router';
import { swipeHandler } from '../../shared/lib/swipeHandler';

const isPWA = ref(false)
onMounted(() => {
  isPWA.value = checkPWA()
})

const router = useRouter()

const { onTouchStart, onTouchEnd } = swipeHandler({ onRightSwipe: () => router.push('/') })

const onClickVibration = () => {
  if (navigator.vibrate) {
    // 200ms振動 → 100ms停止
    navigator.vibrate([200, 100, 200, 100, 200])
    console.log('バイブレーションを実行します')
  } else {
    console.log('バイブレーションはサポートされていません')
  }
}
</script>

<template>
  <h1>About Page</h1>
  <div style="margin-top: 10px; margin-bottom: 10px;">
    <span v-if="isPWA">PWAとして閲覧しています。</span>
    <span v-else>ブラウザとして閲覧しています。</span>
  </div>
  
  <div @touchstart="onTouchStart" @touchend="onTouchEnd" style="height: 80px; width: full; padding: 20px 0 20px 0; background-color: whitesmoke;">
    スワイプするとHomePageに遷移します
  </div>

  <button type="button" class="c-link c-link--red c-link--center" @click="onClickVibration">
    バイブレーション検討ボタン
  </button>
</template>