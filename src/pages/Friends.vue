<!--
 * @FileDescription: 联系人列表页面
 * @Author: Stapxs
 * @Date: 
 *      2022/08/14
 *      2022/12/12
 * @Version:
 *      1.0 - 初始版本
 *      1.5 - 重构为 ts 版本，代码格式优化
-->

<template>
    <div class="friend-view">
        <div :class="'friend-list' + (runtimeData.tags.openSideBar ? ' open' : '')" id="friend-list">
            <div>
                <div class="base">
                    <span>{{ $t('friend_title') }}</span>
                    <div style="flex: 1;"></div>
                    <font-awesome-icon @click="reloadUser" :icon="['fas', 'rotate-right']" />
                </div>
                <div class="small">
                    <label>
                        <input v-model="searchInfo" @input="search" type="text" :placeholder="$t('base_search')">
                        <font-awesome-icon :icon="['fas', 'magnifying-glass']" />
                    </label>
                    <div class="reload" @click="reloadUser">
                        <font-awesome-icon :icon="['fas', 'rotate-right']" />
                    </div>
                    <div @click="openLeftBar"><font-awesome-icon :icon="['fas', 'bars-staggered']" /></div>
                </div>
                <label>
                    <input v-model="searchInfo" @input="search" type="text" :placeholder="$t('base_search')">
                    <font-awesome-icon :icon="['fas', 'magnifying-glass']" />
                </label>
            </div>
            <div :class="(runtimeData.tags.openSideBar ? 'open' : '')">
                <template v-if="runtimeData.showList.length <= 0">
                    <template v-for="info in runtimeData.tags.classes"
                        :key="'class-' + info.class_id">
                        <div :class="'list exp-body' + (classStatus[info.class_id] == true ? ' open' : '')">
                            <header :title="info.class_name" :class="'exp-header' + (runtimeData.tags.openSideBar ? ' open' : '')" @click="classClick(info.class_id)">
                                <div></div>
                                <span>{{ info.class_name }}</span>
                                <a>{{ info.user_count ?? runtimeData.userList.filter((get) => { return get.class_id == info.class_id }).length }}</a>
                            </header>
                            <div :id="'class-' + info.class_id">
                                <FriendBody 
                                    v-for="item in runtimeData.userList.filter((get) => { return get.class_id == info.class_id })"
                                    :key="'fb-' + (item.user_id ? item.user_id : item.group_id)" :data="item"
                                    @click="userClick(item, $event)">
                                </FriendBody>
                            </div>
                        </div>
                    </template>
                    <div :class="'list exp-body' + (classStatus['-1'] == true ? ' open' : '')">
                        <header :title="$t('friend_group')" :class="'exp-header' + (runtimeData.tags.openSideBar ? ' open' : '')" @click="classClick('-1')">
                            <div></div>
                            <span>{{ $t('friend_group') }}</span>
                            <a>{{ runtimeData.userList.filter((get) => { return get.class_id == undefined }).length }}</a>
                        </header>
                        <div>
                            <FriendBody 
                                v-for="item in runtimeData.userList.filter((get) => { return get.class_id == undefined })"
                                :key="'fb-' + (item.user_id ? item.user_id : item.group_id)" :data="item"
                                @click="userClick(item, $event)">
                            </FriendBody>
                        </div>
                    </div>
                </template>
                <!-- 搜索用的 -->
                <div v-else class="list">
                    <div>
                        <FriendBody v-for="item in runtimeData.showList"
                            :key="'fb-' + (item.user_id ? item.user_id : item.group_id)" :data="item"
                            @click="userClick(item, $event)">
                        </FriendBody>
                    </div>
                </div>
            </div>
        </div>
        <div :class="'friend-list-space' + (runtimeData.tags.openSideBar ? ' open' : '')">
            <div class="ss-card">
                <font-awesome-icon :icon="['fas', 'inbox']" />
                <span>{{ $t('chat_space') }}</span>
            </div>
        </div>
    </div>
</template>
  
<script lang="ts">
import FriendBody from '@/components/FriendBody.vue'

import { defineComponent } from 'vue'
import { BaseChatInfoElem, UserFriendElem } from '@/function/elements/information'
import { UserGroupElem } from '@/function/elements/information'

import { runtimeData } from '@/function/msg'
import { reloadUsers } from '@/function/utils/appUtil'

export default defineComponent({
    name: 'ViewFriends',
    components: { FriendBody },
    props: ['list'],
    data () {
        return {
            runtimeData: runtimeData,
            loading: false,
            isSearch: false,
            searchInfo: '',
            classStatus: {} as {[key: string]: boolean}
        }
    },
    methods: {
        /**
         * 联系人被点击事件
         * @param data 联系人信息
         * @param event 点击事件
         */
        userClick (data: UserFriendElem & UserGroupElem, event: Event) {
            const sender = event.currentTarget as HTMLDivElement
            if (this.runtimeData.tags.openSideBar) {
                this.openLeftBar()
            }
            this.isSearch = false
            this.searchInfo = ''
            this.runtimeData.showList = [] as any[]

            const back = {
                type: data.user_id ? 'user' : 'group',
                id: data.user_id ? data.user_id : data.group_id,
                name: this.getShowName(data),
                avatar: data.user_id ? 'https://q1.qlogo.cn/g?b=qq&s=0&nk=' + data.user_id : 'https://p.qlogo.cn/gh/' + data.group_id + '/' + data.group_id + '/0',
                jump: sender.dataset.jump
            } as BaseChatInfoElem
            // 更新聊天框
            this.$emit('userClick', back)
            // 查重
            const getList = runtimeData.onMsgList.filter((item) => {
                const id = item.user_id ? item.user_id : item.group_id
                return Number(id) === Number(back.id)
            })
            if (getList.length === 0) {
                runtimeData.onMsgList.push(data)
            }
            // 获取历史消息
            this.$emit('loadHistory', back)
            // 切换标签卡
            const barMsg = document.getElementById('bar-msg')
            if(barMsg !== null) {
                barMsg.click()
            }
        },
        
        /**
         * 列表搜索
         * @param event 输入事件
         */
        search (event: Event) {
            const value = (event.target as HTMLInputElement).value
            if (value !== '') {
                this.isSearch = true
                this.runtimeData.showList = this.list.filter((item: UserFriendElem & UserGroupElem) => {
                    const name = (item.user_id ? (item.nickname + item.remark) : item.group_name).toLowerCase()
                    const py = item.py_name ? item.py_name : ''
                    const id = item.user_id ? item.user_id : item.group_id
                    return id.toString() === value || (value.length > 4 && py.indexOf(value.toLowerCase()) != -1) || name.indexOf(value.toLowerCase()) != -1
                })
            } else {
                this.isSearch = false
                this.runtimeData.showList = [] as any[]
            }
        },

        /**
         * 重新加载联系人列表
         */
        reloadUser () {
            reloadUsers()
        },

        /**
         * 切换侧边栏状态
         */
        openLeftBar () {
            runtimeData.tags.openSideBar = !runtimeData.tags.openSideBar
        },

        classClick(id: string) {
            if(this.classStatus[id]) {
                this.classStatus[id] = !this.classStatus[id]
            } else {
                this.classStatus[id] = true
            }
        },

        getShowName(data: UserFriendElem & UserGroupElem) {
            const group = data.group_name
            const remark = data.remark
            const nickname = data.nickname
            if(group) return group
            else {
                if(!remark || remark == nickname) {
                    return nickname
                } else {
                    return remark + '（' + nickname + '）'
                }
            }
        }
    }
})
</script>
  
<style scoped>
.exp-header {
    color: var(--color-font);
    align-items: center;
    border-radius: 7px;
    cursor: pointer;
    margin: 0 10px;
    padding: 10px;
    display: flex;
}
.exp-header:hover {
    background: var(--color-card-2);
}
.exp-header > div {
    background: var(--color-main);
    margin-right: 10px;
    border-radius: 7px;
    height: 1rem;
    width: 5px;
}
.exp-header > span {
    flex: 1;
}
.exp-header > a {
    color: var(--color-font-2);
    font-size: 0.9rem;
}

.exp-body > div {
    /* transition: transform .3s;
    transform-origin: top; */
    transform: scaleY(0);
    height: 0;
}
.exp-body.open > div {
    transform: scaleY(1);
    height: unset;
}

@media (max-width: 700px) {
    .exp-header:not(.open) {
        padding: 10px 5px;
    }
    .exp-header:not(.open) > span {
        display: none;
    }
}
</style>
