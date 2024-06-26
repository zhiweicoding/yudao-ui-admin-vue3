<template>
  <div v-loading="loading">
    <div class="flex items-start justify-between">
      <div>
        <!-- 左上：客户基本信息 -->
        <el-col>
          <el-row>
            <span class="text-xl font-bold">{{ customer.name }}【{{ customer.dealStatus ? '已成交' : '未成交' }}】</span>
          </el-row>
        </el-col>
      </div>
      <div>
        <!-- 右上：按钮 -->
        <slot></slot>
      </div>
    </div>
  </div>
  <ContentWrap class="mt-10px">
<!--    <el-descriptions :column="5" direction="vertical">-->
<!--      <el-descriptions-item label="客户级别">-->
<!--        <dict-tag :type="DICT_TYPE.CRM_CUSTOMER_LEVEL" :value="customer.level" />-->
<!--      </el-descriptions-item>-->
<!--      <el-descriptions-item label="成交状态">-->
<!--        {{ customer.dealStatus ? '已成交' : '未成交' }}-->
<!--      </el-descriptions-item>-->
<!--      <el-descriptions-item label="负责人">{{ customer.ownerUserName }}</el-descriptions-item>-->
<!--      <el-descriptions-item label="创建时间">-->
<!--        {{ formatDate(customer.createTime) }}-->
<!--      </el-descriptions-item>-->
<!--    </el-descriptions>-->
    <el-collapse v-model="activeNames" class="">
      <el-collapse-item name="basicInfo">
        <template #title>
          <span class="text-base font-bold">基本信息</span>
        </template>
        <el-descriptions :column="4">
          <el-descriptions-item label="客户名称">
            {{ customer.name }}
          </el-descriptions-item>
          <el-descriptions-item label="客户来源">
            <dict-tag :type="DICT_TYPE.CRM_CUSTOMER_SOURCE" :value="customer.source" />
          </el-descriptions-item>
          <el-descriptions-item label="手机">{{ customer.mobile }}</el-descriptions-item>
          <el-descriptions-item label="电话">{{ customer.telephone }}</el-descriptions-item>
          <el-descriptions-item label="邮箱">{{ customer.email }}</el-descriptions-item>
          <el-descriptions-item label="地址">
            {{ customer.areaName }} {{ customer.detailAddress }}
          </el-descriptions-item>
          <el-descriptions-item label="QQ">{{ customer.qq }}</el-descriptions-item>
          <el-descriptions-item label="微信">{{ customer.wechat }}</el-descriptions-item>
          <el-descriptions-item label="客户行业">
            <dict-tag :type="DICT_TYPE.CRM_CUSTOMER_INDUSTRY" :value="customer.industryId" />
          </el-descriptions-item>
          <el-descriptions-item label="客户级别">
            <dict-tag :type="DICT_TYPE.CRM_CUSTOMER_LEVEL" :value="customer.level" />
          </el-descriptions-item>
          <el-descriptions-item label="下次联系时间">
            {{ formatDate(customer.contactNextTime) }}
          </el-descriptions-item>
          <el-descriptions-item label="备注">{{ customer.remark }}</el-descriptions-item>
        </el-descriptions>
      </el-collapse-item>
      <el-collapse-item name="systemInfo">
        <template #title>
          <span class="text-base font-bold">系统信息</span>
        </template>
        <el-descriptions :column="4">
          <el-descriptions-item label="负责人">{{ customer.ownerUserName }}</el-descriptions-item>
          <el-descriptions-item label="最后跟进记录">
            {{ customer.contactLastContent }}
          </el-descriptions-item>
          <el-descriptions-item label="最后跟进时间">
            {{ formatDate(customer.contactLastTime) }}
          </el-descriptions-item>
          <el-descriptions-item label="">&nbsp;</el-descriptions-item>
          <el-descriptions-item label="创建人">{{ customer.creatorName }}</el-descriptions-item>
          <el-descriptions-item label="创建时间">
            {{ formatDate(customer.createTime) }}
          </el-descriptions-item>
          <el-descriptions-item label="更新时间">
            {{ formatDate(customer.updateTime) }}
          </el-descriptions-item>
        </el-descriptions>
      </el-collapse-item>
    </el-collapse>
  </ContentWrap>
</template>
<script lang="ts" setup>
import { DICT_TYPE } from '@/utils/dict'
import * as CustomerApi from '@/api/crm/customer'
import { formatDate } from '@/utils/formatTime'

defineOptions({ name: 'CrmCustomerDetailsHeader' })
defineProps<{
  customer: CustomerApi.CustomerVO // 客户信息
  loading: boolean // 加载中
}>()
const activeNames = ref(['basicInfo', 'systemInfo']) // 展示的折叠面板
</script>
