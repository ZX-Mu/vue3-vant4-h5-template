<script setup lang="ts" name="Tools">
import { getListApi, getListApiError } from '@/api/mock'
import { reactive } from 'vue'
import { showFailToast, showSuccessToast } from 'vant'
import 'vant/es/toast/style'

const showList: string[] = reactive([])

const handleSuccessReq = async () => {
  const { list } = await getListApi()
  showSuccessToast('请求成功')
  showList.push(...list)
}
const handleErrorReq = () => {
  getListApiError().then(
    () => {},
    err => {
      console.log(err)
      showFailToast('请求有误')
    }
  )
}
</script>

<template>
  <div class="tools-content pt-[20px] px-[12px]">
    <!-- Mock -->
    <div class="pl-[12px] border-l-[3px] border-[color:#41b883] mb-[12px]">
      <h3 class="font-bold text-[18px] my-[4px]">Mock</h3>
    </div>
    <van-space>
      <van-button type="success" @click="handleSuccessReq">成功请求</van-button>
      <van-button type="danger" @click="handleErrorReq">失败请求</van-button>
    </van-space>
    <div class="text-[14px] py-[2px] px-[10px] rounded-[4px] bg-[var(--color-block-background)] mt-[14px]">
      <p class="my-[14px] leading-[24px]">
        {{ showList }}
      </p>
    </div>
    <!-- Icon -->
    <div class="pl-[12px] border-l-[3px] border-[color:#41b883] mt-[24px] mb-[12px]">
      <h3 class="font-bold text-[18px] my-[4px]">Iconify Icon</h3>
    </div>
    <!-- offline iconify icon -->
    <div class="mt-2">
      <i-icon icon="material-symbols:contact-support-outline-rounded" class="inline-block text-[24px] mr-3" />
    </div>
    <div class="pl-[12px] border-l-[3px] border-[color:#41b883] mt-[24px] mb-[12px]">
      <h3 class="font-bold text-[18px] my-[4px]">Svg Icon</h3>
    </div>
    <!-- local svg file icon -->
    <div>
      <svg-icon name="light" class="inline-block text-[24px] mr-3" />
    </div>
  </div>
</template>
