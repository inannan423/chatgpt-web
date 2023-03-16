<script setup lang='ts'>
import { onMounted, ref } from 'vue'
import { NSpin } from 'naive-ui'
import { fetchChatConfig } from '@/api'

interface ConfigState {
  timeoutMs?: number
  reverseProxy?: string
  apiModel?: string
  socksProxy?: string
  httpsProxy?: string
}

const loading = ref(false)

const config = ref<ConfigState>()

async function fetchConfig() {
  try {
    loading.value = true
    const { data } = await fetchChatConfig<ConfigState>()
    config.value = data
  }
  finally {
    loading.value = false
  }
}

onMounted(() => {
  fetchConfig()
})
</script>

<template>
  <NSpin :show="loading">
    <div class="p-4 space-y-4">
      <div class="p-2 space-y-2 rounded-md bg-neutral-100 dark:bg-neutral-700">
        <p>
          ❤ 基于
          <a
            class="text-blue-600 dark:text-blue-500"
            href="https://github.com/Chanzhaoyu/chatgpt-web"
            target="_blank"
          >
            Github Chanzhaoyu
          </a>
          及贡献者的开源代码，感谢开源世界的每一位贡献者。
        </p>
        <p>
          📕 MIT License
        </p>
        <p>
          🤖 Served by
          <a
            class="text-blue-600 dark:text-blue-500"
            href="https://github.com/inannan423"
            target="_blank"
          >
            CZH
          </a>
        </p>
      </div>
      <h2 class="text-xl font-bold">
        说明
      </h2>
      <p>
        OpenAI 会赠送每个账号 18 美元 API 调用额度，API 额度消费完之后，本项目将停止运营。因此请不要滥用 API，让更多的人能体验。
        如果你有闲置的 API 额度，可以联系我，为这个项目续命。本项目基于开源代码构建并完全开源，不会进行任何盈利活动。
      </p>
      <p class="text-gray-400">
        禁止将本项目用于任何不当用途，否则后果自负。
      </p>
      <p>
        WeChat: Orange_inannan
      </p>
      <p>
        My Blog: <a class="text-green-500" href="https://jetzihan.netlify.app/" target="_blank">Blog</a>
      </p>
      <p>
        My GitHub: <a class="text-green-500" href="https://github.com/inannan423" target="_blank">GitHub</a>
      </p>
    </div>
  </NSpin>
</template>
