<script setup lang="ts">
import { onMounted } from 'vue'
import { SimplePlayer, Events } from 'xgplayer'
import Player from 'xgplayer'
import defaultPresetEn from 'xgplayer/es/presets/default-en'
import 'xgplayer/dist/index.min.css'
import IC from './favicon.ico'
import VideoCard from './components/VideoCard.vue'
import { ref } from 'vue'

// 模拟卡片列表数据（实际项目可从接口获取）
const cardList = ref([
  {
    image: 'https://picsum.photos/id/10/400/225',
    title: '风景卡片1',
    desc: '这是一片宁静的湖泊，周围环绕着青山，适合周末露营。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
  {
    image: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    title: '美食卡片',
    desc: '手工制作的意大利面，搭配新鲜番茄酱汁和香草，口感丰富。',
  },
])

onMounted(() => {
  SimplePlayer.defaultPreset = defaultPresetEn

  const thumbnail = {
    urls: [], // 雪碧图url列表
    pic_num: 128, // 预览图总帧数
    row: 10, // 每张雪碧图包含的预览图行数
    col: 10, // 每张雪碧图包含的预览图列数
    height: 160, // 预览图每一帧的高度（单位：px）
    width: 90, // 预览图每一帧的宽度（单位：px）
  }

  const player = new SimplePlayer({
    id: 'vs',
    lang: 'zh',
    volume: 0,
    // autoplay: true,
    // autoplayMuted: true,
    // screenShot: true,
    // defaultPlaybackRate: 2.0,
    // loop: true,
    // startTime: 40,
    url: [
      {
        src: 'http://s2.pstatp.com/cdn/expire-1-M/byted-player-videos/1.0.0/xgplayer-demo.mp4',
        type: 'video/mp4',
      },
      {
        src: 'http://s2.pstatp.com/cdn/expire-1-M/byted-player-videos/1.0.0/xgplayer-demo.mp4',
        type: 'video/mp4',
      },
    ],
    poster: 'https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg',
    // fluid: true, // 填满屏幕 （流式布局）
    playbackRate: [0.5, 0.75, 1, 1.5, 2], //传入倍速可选数组
    // height: '100%',
    // width: '100%',
    // width: 1280,
    // height: 600,
    // fitVideoSize: 'fixHeight',
    playsinline: true,
    progressDot: [
      {
        id: 0, // 唯一标识，用于删除的时候索引
        time: 10, // 展示的时间点，例子为在播放到10s钟的时候展示
        text: '你是傻子', // hover的时候展示文案，可以为空
        duration: 1, // 展示时间跨度，单位为s
        style: {
          // 指定样式
          backgroundColor: 'yellow',
        },
      },
    ],
    thumbnail: thumbnail,
    marginControls: false,
    fullscreenTarget: document.querySelector('.container'),
    closeFocusVideoFocus: true,
    closeVideoClick: true,
    icons: {
      play: IC,
    },
  })

  player.on(Events.AUTOPLAY_PREVENTED, () => {
    console.log('autoplay was prevented!!')
  })

  player.on(Events.AUTOPLAY_STARTED, () => {
    console.log('autoplay success!!')
  })

  const result = Player.isHevcSupported()
  console.log(result ? 'support h265!' : "Don't support!")
})
</script>

<template>
  <div class="card-list">
    <!-- 单个卡片：传入自定义图片、标题、描述 -->
    <!-- <VideoCard
      image-src="https://i.ytimg.com/vi/7J653nwumcw/hq720.jpg"
      imageAlt="小狗图片"
      title="可爱宠物卡片"
      description="这是一只活泼的小狗，喜欢玩球和晒太阳，适合家庭饲养。"
    /> -->
    <el-row :gutter="50">
      <!-- <el-col :span="12"> -->
      <VideoCard
        v-for="(item, index) in cardList"
        :key="index"
        :image-src="item.image"
        :image-alt="item.title"
        :description="item.desc"
      >
      </VideoCard>
      <!-- </el-col> -->
    </el-row>
  </div>
</template>

<style scoped>
#vs {
  flex: auto;
}

.video-card {
  padding: 10px;
}
</style>
