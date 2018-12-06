<template>
    <div class="">
        <van-cell
                v-for="(value,key) in web_frame_list"
                v-if="value.title!==''"
                :key="key"
                @tap="popup_info(value.description)"
        >
            <view slot="title">
                <image :src="value.thumb"
                    style="float:left;display: block;;width: 70rpx;height:70rpx;margin-right: 10rpx;" lazy-load
                ></image>
                <span class="van-cell-text">{{value.title}}</span>
                <span style="float: right;margin-right: 5rpx;margin-top: 5rpx">
                    <van-icon name="arrow" />
                </span>
                <span style="float: right;margin-right: 15rpx;">
                    {{value.index}}
                </span>
            </view>
        </van-cell>

        <van-popup
                :show="show"
                :close="onClose"
                :close-on-click-overlay="true"
                @clickOverlay="click_overlay"
                custom-class="custom_style"
                :overlay="true"
                @close="onClose"
        >

            {{description}}
        </van-popup>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                web_frame_list: [],
                show: false,
                description: '',
        }
        },
        onLoad(){
            let url = "http://localhost:3001/api/web_frame";
            wx.request({
                url: url,
                data: {
                    // x: '',
                },
                header: {
                    'content-type': 'application/json' // 默认值
                },
                success: (res) => {
                    console.log(res.data);
                    if(res.data.code === 200){
                        console.log("已获取排行信息。");
                        this.web_frame_list = res.data.data;
                    }
                },fail (e){
                    console.log(e.errMsg);
                }
            })
        },
        methods: {
            click_overlay(){
              console.log("用户点击了遮罩");
            },
            onClose(){
                this.show = false;
              console.log("弹出层已经关闭");
            },
            popup_info(description){
                console.log("开始展示弹出层");
                this.description = description;
                this.show = true;
            },
            jump_content(index){
            }
        },
    }
</script>

<style>
    .van-cell-text{
        font-weight: bold;
        font-size: 40rpx;

        float:left;
        margin-left:15rpx;
        margin-top:4rpx;
    }
    .custom_style{
        padding: 30rpx;
    }

</style>
