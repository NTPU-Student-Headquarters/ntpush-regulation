<script setup lang="ts">
definePageMeta({
  layout: 'cloud'
})

const isLoggingIn = ref(false)

// 模擬 Google 登入流程
const handleGoogleLogin = () => {
  isLoggingIn.value = true
  
  // 實際開發：這裡會導向後端的 OAuth Endpoint，例如 /api/auth/google
  // window.location.href = '/api/auth/google'
  
  // 模擬：2秒後成功登入
  setTimeout(() => {
    // 假設後端驗證了 .env 中的 ALLOWED_EMAILS 並回傳了 token
    const mockUser = {
      name: '自治幹部A',
      email: 'ntpusa@gm.ntpu.edu.tw',
      department: '學生會行政中心',
      avatar: ''
    }
    const user = useUser()
    user.value = mockUser
    isLoggingIn.value = false
    navigateTo('/')
  }, 1500)
}
</script>

<template>
  <div class="flex-grow flex items-center justify-center -mt-16"> <!-- -mt-16 to center vertically considering header -->
    <div class="w-full max-w-sm">
      
      <div class="bg-white dark:bg-slate-800 rounded-[28px] shadow-xl border border-slate-100 dark:border-slate-700 overflow-hidden p-8 text-center">
        
        <!-- Icon -->
        <div class="w-16 h-16 bg-blue-50 dark:bg-blue-900/30 rounded-2xl mx-auto flex items-center justify-center mb-6">
          <span class="material-symbols-rounded text-4xl text-blue-600 dark:text-blue-400">admin_panel_settings</span>
        </div>

        <h2 class="text-2xl font-bold mb-3 text-slate-800 dark:text-slate-100">自治夥伴登入</h2>
        <p class="text-slate-500 dark:text-slate-400 text-sm mb-8 leading-relaxed">
          本系統僅限國立臺北大學學生自治組織<br>
          內部人員使用，請使用授權信箱登入。
        </p>

        <!-- Google Login Button -->
        <button 
          @click="handleGoogleLogin"
          :disabled="isLoggingIn"
          class="w-full relative flex items-center justify-center gap-3 bg-white dark:bg-[#131314] text-slate-700 dark:text-slate-200 border border-slate-300 dark:border-slate-600 hover:bg-slate-50 dark:hover:bg-slate-800 active:bg-slate-100 transition-all rounded-full px-6 py-3.5 shadow-sm group"
        >
          <img src="https://www.svgrepo.com/show/475656/google-color.svg" class="w-5 h-5" alt="Google Logo">
          <span class="font-medium tracking-wide">
            {{ isLoggingIn ? '正在驗證身分...' : '使用 Google 帳號登入' }}
          </span>
          
          <!-- Loading Spinner -->
          <div v-if="isLoggingIn" class="absolute right-4 w-4 h-4 border-2 border-slate-300 border-t-blue-600 rounded-full animate-spin"></div>
        </button>

        <!-- 警語 -->
        <div class="mt-8 pt-6 border-t border-slate-100 dark:border-slate-700">
          <div class="flex items-start gap-2 text-left">
            <span class="material-symbols-rounded text-amber-500 text-lg mt-0.5">warning</span>
            <p class="text-xs text-slate-400 dark:text-slate-500">
              非授權帳號將無法通過驗證。若您是新進幹部且無法登入，請聯繫秘書部或資訊長更新白名單權限。
            </p>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>