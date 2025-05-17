<template>
  <view class="login-container">
    <view class="login-header u-flex u-row-between u-p-20">
      <view class="back-icon">
        <u-icon name="arrow-left" size="20" color="#fff"></u-icon>
      </view>
      <view class="logo">
        <u-icon name="home" size="30" color="#e60012"></u-icon>
      </view>
      <view class="user-info">
        <u-icon name="user" size="20" color="#fff"></u-icon>
      </view>
    </view>

    <view class="login-body u-p-30">
      <view class="login-title u-font-32 u-m-b-40">
        <text>登录</text>
      </view>

      <u-form ref="loginForm" :model="loginForm" :rules="rules" label-width="0">
        <u-form-item prop="phone">
          <u-input
            v-model="loginForm.phone"
            placeholder="请输入手机号"
            prefix-icon="mobile"
            border
          />
        </u-form-item>
        <u-form-item prop="password">
          <u-input
            v-model="loginForm.password"
            type="password"
            placeholder="请输入密码"
            prefix-icon="lock"
            border
          />
        </u-form-item>
        <u-form-item prop="role">
          <u-select
            mode="single-column"
            :list="roleList"
            v-model="loginForm.role"
            placeholder="请选择角色"
          ></u-select>
        </u-form-item>
      </u-form>

      <view class="login-btn u-m-t-40">
        <u-button type="error" text="登录" @click="submitForm('loginForm')" block></u-button>
      </view>

      <view class="login-links u-flex u-row-between u-m-t-30">
        <text @click="forgotPassword" class="u-tips">忘记密码？</text>
        <text @click="register" class="u-tips">新用户注册</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      loginForm: {
        phone: '',
        password: '',
        role: null
      },
      rules: {
        phone: [
          {
            required: true,
            message: '请输入手机号',
            trigger: 'blur'
          },
          {
            pattern: /^1[3-9]\d{9}$/,
            message: '请输入正确的手机号格式',
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: '请输入密码',
            trigger: 'blur'
          },
          {
            min: 6,
            max: 16,
            message: '密码长度在6到16个字符之间',
            trigger: 'blur'
          }
        ],
        role: [
          {
            required: true,
            message: '请选择角色',
            trigger: 'change'
          }
        ]
      },
      roleList: [
        {
          value: 'student',
          label: '学生'
        },
        {
          value: 'teacher',
          label: '教师'
        },
        {
          value: 'admin',
          label: '管理员'
        }
      ]
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          // 模拟登录请求
          if (this.loginForm.phone === '13800138000' && this.loginForm.password === '123456') {
            this.$u.toast('登录成功');
            // 模拟登录成功后跳转到消息页面
            this.$u.route({
              url: 'pages/messages/messages'
            });
          } else {
            this.$u.toast('手机号或密码错误');
          }
        } else {
          console.log('验证失败!');
          return false;
        }
      });
    },
    forgotPassword() {
      // 跳转到忘记密码页面
      this.$u.route({
        url: 'pages/forgot-password/forgot-password'
      });
    },
    register() {
      // 跳转到注册页面
      this.$u.route({
        url: 'pages/register/register'
      });
    }
  }
};
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  background-color: #f5f5f5;
}

.login-header {
  background-color: #e60012;
  color: white;
}

.login-body {
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.login-title {
  font-weight: bold;
  text-align: center;
  color: #333;
}

.login-links {
  font-size: 14px;
  color: #e60012;
}
</style>