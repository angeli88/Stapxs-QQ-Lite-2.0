<!--
 * @FileDescription: 关于模板
 * @Author: Stapxs
 * @Date: 2024/04/22
 * @Version: 1.0
-->

<template>
    <div class="about-pan">
        <div id="logo-card" :class="'ss-card logo-card' + (showUI ? '' : ' hidd-sha')">
            <svg viewBox="0 0 1080 1080" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M537 1080C833.577 1080 1074 839.577 1074 543C1074 246.423 833.577 6 537 6C240.423 6 0 246.423 0 543C0 839.577 240.423 1080 537 1080Z"/>
                <path d="M540.28 803.2C493.78 803.2 451.18 787.7 423.68 764.4C409.78 768.6 391.88 775.3 380.68 783.6C371.08 790.7 372.28 798 373.98 800.9C381.58 813.8 504.68 809.1 540.28 805.1V803.2ZM540.28 803.2C586.78 803.2 629.38 787.7 656.88 764.4C670.78 768.6 688.68 775.3 699.88 783.6C709.48 790.7 708.28 798 706.58 800.9C698.98 813.8 575.88 809.1 540.28 805.1V803.2Z" fill="#F8F9FA"/>
                <path d="M540.58 524.8C617.28 524.3 678.78 509.4 699.58 503.7C704.58 502.3 707.18 499.9 707.18 499.9C707.18 499.2 707.48 487.4 707.48 481.3C707.48 378.9 659.18 276 540.18 276C421.28 276 372.88 378.9 372.88 481.3C372.88 487.4 373.18 499.2 373.18 499.9C373.18 499.9 375.38 502.2 379.28 503.3C398.48 508.7 461.18 524.2 539.78 524.8H540.58ZM749.08 610.1C744.28 594.8 737.88 576.9 731.28 559.8C731.28 559.8 727.48 559.3 725.58 559.9C666.58 577 595.08 588 540.58 587.3H539.98C485.78 587.9 414.78 577.2 355.98 560.2C353.78 559.6 349.28 559.8 349.28 559.8C342.68 576.9 336.18 594.8 331.48 610.1C308.78 683.1 316.18 713.3 321.78 714C333.78 715.5 368.48 659.1 368.48 659.1C368.48 716.4 420.18 804.4 538.68 805.2H541.78C660.28 804.4 711.98 716.4 711.98 659.1C711.98 659.1 746.68 715.5 758.68 714C764.38 713.3 771.68 683.1 749.08 610.1Z" fill="#F8F9FA"/>
                <path d="M497.98 427.3C481.88 428 468.08 409.7 467.18 386.3C466.28 362.9 478.68 343.4 494.78 342.7C510.88 342 524.68 360.3 525.58 383.7C526.48 407.1 514.08 426.6 497.98 427.3ZM613.38 386.3C612.48 409.7 598.78 428 582.58 427.3C566.48 426.6 554.08 407 554.98 383.7C555.88 360.3 569.58 342 585.78 342.7C601.88 343.4 614.28 362.9 613.38 386.3Z" fill="#F8F9FA"/>
                <path d="M517.78 386.7C518.48 395.9 513.48 404.1 506.48 405C499.48 405.9 493.28 399.1 492.48 389.9C491.78 380.7 496.78 372.5 503.78 371.6C510.78 370.7 517.08 377.4 517.78 386.7ZM562.08 389.7C563.48 387.1 573.18 373.7 593.28 378.6C598.58 379.9 600.98 381.8 601.48 382.5C602.28 383.6 602.48 385.2 601.68 387.3C600.18 391.5 596.98 391.4 595.28 390.5C594.18 390 580.18 380.6 567.28 394.6C566.38 395.6 564.78 395.9 563.28 394.7C561.88 393.6 561.28 391.3 562.08 389.7Z" fill="#F8F9FA"/>
                <path d="M540.58 583.9H539.98C502.88 584.3 457.98 579.4 414.48 570.9C410.78 592.5 408.48 619.6 410.48 651.9C415.38 733.6 463.88 785 538.78 785.7H541.78C616.68 785 665.18 733.6 670.08 651.9C671.98 619.6 669.78 592.5 666.08 570.9C622.58 579.5 577.68 584.4 540.58 583.9Z" fill="#F8F9FA"/>
                <path d="M435.08 577.1V657.5C435.08 657.5 471.88 664.9 508.78 659.8V585.6C485.38 584.3 460.18 581.4 435.08 577.1Z" fill="#E9EBED"/>
                <path d="M707.28 499.9C707.28 499.9 635.68 522.5 540.58 523.2H539.98C445.08 522.6 373.58 500 373.28 499.9L349.28 559.8C409.28 577.9 483.68 589.6 539.88 588.9H540.48C596.68 589.6 671.08 577.9 731.18 559.8L707.28 499.9Z" fill="#E9EBED"/>
            </svg>
            <div>
                <span>{{ $t('name') }}</span>
                <a>2.0</a>
            </div>
            <span style="text-align: center;">{{ $t('description') }}</span>
            <a>v{{ packageInfo.version }}</a>
            <div class="buttons">
                <a class="ss-button" @click="goGithub()">{{
                $t('option_info_visit_github') }}</a>
                <a class="ss-button" style="width: 30px;" @click="goBlog()">
                    <font-awesome-icon :icon="['fas', 'circle-info']"/>
                </a>
            </div>
            <div v-if="constList.length > 0" class="ss-card contributors-card">
                <div>
                    <div v-for="info in constList" :key="'contributors-' + info.title" :title="info.title"
                        :style="'background-image: url(' + info.url + ');'" :class="(info.isMe ? 'me' : '') + (info.isSuperThakns ? ' super-thanks' : '')"
                        @click="openLink(info.link)"></div>
                </div>
            </div>
        </div>
        <div class="ss-card jump-card" @click="dependencies" :style="showUI ? '' : 'background: var(--color-card-1);'">
            <header><div></div>{{ $t('list_of_dependencies') }}</header>
            <font-awesome-icon :icon="['fas', 'angle-right']"/>
        </div>
        <div v-if="showUI" class="ss-card bcd-about" @click="openLink('https://stapxs.github.io/Border-Card-UI/docs/')">
            <div>
                <div>
                    <div class="bcd-body"
                        style="width: 45%;display: flex;justify-content: flex-end;border-radius: 0 5px 0 0;">
                        <div
                            style="background:var(--color-card-2);border-radius: 16px;width: 25%;margin: 5px 0 5px 5px;">
                        </div>
                        <div
                            style="background: var(--color-card-2);border-radius: 100%;width: 7px;margin: 5px 8px 5px 5px;">
                        </div>
                    </div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 20%;margin-right: 25%;"></div>
                    <div class="bcd-body" style="width: 55%;display: flex;justify-content: flex-end;">
                        <div
                            style="background: var(--color-card-2);width: calc(25% + 26px);margin-right: 5px;border-radius: 5px 5px 0 0;display: flex;justify-content: flex-end;">
                            <div
                                style="background:var(--color-main);border-radius: 100%;width: 7px;margin: 10px 5px 0 5px;">
                            </div>
                            <div
                                style="background:var(--color-card-1);border-radius: 16px;width: calc(100% - 25px);margin: 10px 7px 0 0;">
                            </div>
                        </div>
                    </div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 10%;margin-right: 20%;"></div>
                    <div class="bcd-body" style="width: 40%;display: flex;justify-content: flex-end;">
                        <div
                            style="background: var(--color-card-2);width: calc(35% + 25px);margin-right: 5px;display: flex;justify-content: flex-end;">
                            <div
                                style="background: var(--color-card-1);border-radius: 16px;width: calc(100% - 14px);height: calc(100% - 10px);margin-top: 2.5px;margin-right: 7px;">
                            </div>
                        </div>
                    </div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 15%;margin-right: 40%;"></div>
                    <div class="bcd-body" style="width: 35%;display: flex;justify-content: flex-end;">
                        <div
                            style="background: var(--color-card-2);width: calc(40% + 25px);margin-right: 5px;border-radius: 0 0 5px 5px;">
                        </div>
                    </div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 43%;"></div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 13%;margin-right: 20%;"></div>
                    <div class="bcd-body" style="width: 49%;"></div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 57%;"></div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 17%;margin-right: 26%;"></div>
                    <div class="bcd-body" style="width: 52%;"></div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 8%;margin-right: 8%;"></div>
                    <div class="bcd-body" style="width: 60%;">
                        <div
                            style="background: var(--color-card-2);width: calc(100% - 7px);height: calc(100% - 7px);margin-top: 7px;border-radius: 0 7px 0 0;">
                        </div>
                    </div>
                </div>
                <div>
                    <div class="bcd-body" style="width: 40%;border-radius: 0 0 7px 0;">
                        <div
                            style="background: var(--color-card-2);width: calc(100% - 7px);height: calc(100% - 7px);margin-right: 7px;border-radius: 0 0 7px 0;">
                        </div>
                    </div>
                </div>
            </div>
            <span>Border Card UI For Web</span>
            <br>
            <a>version rolling</a>
        </div>
    </div>
</template>

<script lang="ts">
import Umami from '@stapxs/umami-logger-typescript'
import DepPan from './DepPan.vue'
import packageInfo from '../../package.json'

import { defineComponent } from 'vue'
import { openLink } from '@/function/utils/appUtil'
import { ContributorElem } from '@/function/elements/system'

import { runtimeData } from '@/function/msg'

export default defineComponent({
    name: 'AboutPan',
    props: {
        showUI: {
            type: Boolean,
            default: false
        }
    },
    data() {
        return {
            packageInfo: packageInfo,
            openLink: openLink,
            constList: [] as ContributorElem[]
        }
    },
    methods: {
        dependencies() {
            runtimeData.popBoxList = []
            const popInfo = {
                    title: this.$t('list_of_dependencies'),
                    template: DepPan
                }
                runtimeData.popBoxList.push(popInfo)
        },

        goGithub() {
            openLink('https://github.com/Stapxs/Stapxs-QQ-Lite-2.0')
            // UM：统计点击事件
            Umami.trackEvent('click_statistics', { name: 'visit_github' })
        },

        goBlog() {
            openLink('https://blog.stapxs.cn/About.html')
            // UM：统计点击事件
            Umami.trackEvent('click_statistics', { name: 'visit_blog' })
        }
    },
    mounted() {
        const superThanks = [
            'doodlehuang'
        ]
        // 加载贡献者信息
        fetch('https://api.github.com/repos/stapxs/stapxs-qq-lite-2.0/contributors')
            .then(response => response.json())
            .then((data: { [key: string]: string }[]) => {
                for (let i = 0; i < data.length; i++) {
                    this.constList.push({
                        url: data[i].avatar_url,
                        link: data[i].html_url,
                        title: data[i].login,
                        isMe: data[i].login == 'Stapxs',
                        isSuperThakns: superThanks.includes(data[i].login)
                    })
                }
            })
            .catch(console.error)
    }
})
</script>

<style>
.hidd-sha {
    box-shadow: none !important;
}
</style>
