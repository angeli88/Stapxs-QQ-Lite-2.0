<!--
 * @FileDescription: 公告列表项模板
 * @Author: Stapxs
 * @Date: 2022-12-01
 * @Version: 1.0
-->

<template>
    <div class="base" @click="showAll = !showAll">
        <header>
            <font-awesome-icon :icon="['fas', 'bookmark']"/>
            <span>{{ $t('chat_chat_info_notice') }}</span>
            <div style="flex: 1;"></div>
            <span>{{ Intl.DateTimeFormat(trueLang, { month: "short", day: "numeric", hour: "numeric", minute: "numeric" })
                    .format(data.time) }}</span>
        </header>
        <div :id="'bulletins-msg-' + index" :class="'body' + (!showAll ? '' : ' all')">
            <span v-html="Xss(data.content).replaceAll('\r', '\n').replaceAll('\n\n', '\n')"></span>
        </div>
        <span v-show="needShow && !showAll">{{ $t('bulletin_show_tip') }}</span>
        <div class="info">
            <img :src="'https://q1.qlogo.cn/g?b=qq&s=0&nk=' + data.sender">
            <a>{{ (runtimeData.chatInfo.info.group_members.filter((item) => {
                return Number(item.user_id) ===
                    Number(data.sender)
            }))[0].nickname }}</a>
            <div></div>
            <span v-if="data.is_read">{{
                $t('chat_chat_info_bulletin_read', {
                    isRead: data.is_read ? $t('chat_chat_info_bulletin_readed') : $t('chat_chat_info_bulletin_noread'),
                readNum: data.read_num
            })
            }}</span>
        </div>
    </div>
</template>

<script lang="ts">
import Xss from 'xss'
import { defineComponent } from 'vue'
import { runtimeData } from '@/function/msg'
import { getTrueLang } from '@/function/utils/systemUtil'

export default defineComponent({
    name: 'BulletinBody',
    props: ['data', 'index'],
    data() {
        return {
            trueLang: getTrueLang(),
            Xss: Xss,
            runtimeData: runtimeData,
            showAll: false,
            needShow: true
        }
    },
    mounted() {
        this.$nextTick(() => {
            const tab1 = document.getElementById('info-pan-notices')
            const tab2 = document.getElementById('info-pan-mumber')
            const pan = document.getElementById('bulletins-msg-' + this.index)
            if(pan && tab1 && tab2) {
                // PS：display none 不渲染无法获取实际高度
                tab1.click()
                let maxHeight = Number(getComputedStyle(pan).maxHeight.replace('px', ''))
                const height = pan.offsetHeight
                tab2.click()
                this.needShow = height == maxHeight
            }
        })
    }
})
</script>
