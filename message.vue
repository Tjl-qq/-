<template>
  <view class="messages-container">
    <view class="messages-header u-flex u-row-between u-p-20">
      <view class="back-icon">
        <u-icon name="arrow-left" size="20" color="#fff"></u-icon>
      </view>
      <view class="logo">
        <u-icon name="home" size="30" color="#e60012"></u-icon>
      </view>
      <view class="search-icon">
        <u-icon name="search" size="20" color="#fff"></u-icon>
      </view>
    </view>

    <view class="messages-title u-flex u-row-between u-p-20">
      <view class="title u-font-32">
        <text>消息</text>
      </view>
      <view class="search">
        <u-icon name="search" size="20" color="#333"></u-icon>
      </view>
    </view>

    <view class="messages-list u-p-20">
      <view
        class="message-item u-flex u-row-between"
        v-for="(message, index) in messages"
        :key="index"
        @click="viewMessage(message)"
      >
        <view class="message-icon">
          <u-icon :name="getIcon(message.type)" size="40" color="#fff"></u-icon>
        </view>
        <view class="message-content u-flex-1 u-m-l-20">
          <view class="message-title u-flex u-row-between">
            <view class="title u-font-16">{{ message.title }}</view>
            <view class="time u-font-12 u-type-info">{{ message.time }}</view>
          </view>
          <view class="message-text u-font-14 u-m-t-10">{{ message.text }}</view>
        </view>
      </view>
    </view>

    <view class="bottom-nav u-flex u-row-between u-p-20">
      <view class="nav-item" :class="{ active: activeTab === 'home' }">
        <u-icon name="home" size="24"></u-icon>
        <text>首页</text>
      </view>
      <view class="nav-item" :class="{ active: activeTab === 'study' }">
        <u-icon name="chat" size="24"></u-icon>
        <text>学习</text>
      </view>
      <view class="nav-item" :class="{ active: activeTab === 'messages' }">
        <u-icon name="bell" size="24"></u-icon>
        <text>消息</text>
      </view>
      <view class="nav-item" :class="{ active: activeTab === 'profile' }">
        <u-icon name="account" size="24"></u-icon>
        <text>我的</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 'messages',
      messages: [
        {
          title: '关于开展"学党史、强信念、跟党走"主题团日活动的通知',
          time: '10:30',
          text: '各团支部：根据上级团委要求，定于本周五下午2点在大学生活动中心开展主题团日活动',
          type: 'bell'
        },
        {
          title: '青年大学习第15期学习提醒',
          time: '昨天',
          text: '本周的青年大学习主题是"新时代的中国青年"，请各位同学在周五前完成学习并提交截图',
          type: 'note'
        },
        {
          title: '"红色记忆"党史知识竞赛活动报名通知',
          time: '昨天',
          text: '为庆祝建党102周年，校团委将于下月举办党史知识竞赛，获奖者将获得荣誉证书和奖品',
          type: 'ticket'
        },
        {
          title: '入党积极分子培训班开班通知',
          time: '周一',
          text: '2025年第二期入党积极分子培训班将于6月15日开班，请已通过审核的同学按时参加培训...',
          type: 'peoples'
        },
        {
          title: '优秀党员评选结果公示',
          time: '6月5日',
          text: '恭喜2025年度优秀共产党员评选结果已公示，请登录系统查看',
          type: 'trophy'
        },
        {
          title: '思想汇报提交提醒',
          time: '6月3日',
          text: '请各位入党积极分子和预备党员在6月10日前提交本季度思想汇报，逾期将影响考核...',
          type: 'warning'
        },
        {
          title: '"红色影视赏析"活动预告',
          time: '5月28日',
          text: '下周三晚7点将在图书馆报告厅放映电影《建党伟业》，欢迎同学们前来观看...',
          type: 'video'
        }
      ]
    };
  },
  methods: {
    getIcon(type) {
      const iconMap = {
        bell: 'bell',
        note: 'note',
        ticket: 'ticket',
        peoples: 'peoples',
        trophy: 'trophy',
        warning: 'warning',
        video: 'video'
      };
      return iconMap[type] || 'info';
    },
    viewMessage(message) {
      // 跳转到消息详情页
      this.$u.route({
        url: 'pages/message-detail/message-detail',
        params: {
          id: message.id
        }
      });
    }
  },
  mounted() {
    // 检查登录状态
    const token = uni.getStorageSync('token');
    if (!token) {
      // 如果未登录，跳转到登录页面
      this.$u.route({
        url: 'pages/login/login'
      });
    }
  }
};
</script>

<style scoped>
.messages-container {
  min-height: 100vh;
  background-color: #f5f5f5;
}

.messages-header {
  background-color: #e60012;
}

.message-item {
  background-color: white;
  border-radius: 10px;
  padding: 15px;
  margin-bottom: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
}

.message-icon {
  background-color: #e60012;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
}

.message-title {
  margin-bottom: 5px;
}

.bottom-nav {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: white;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.nav-item text {
  font-size: 12px;
  margin-top: 5px;
}

.nav-item.active {
  color: #e60012;
}
</style>