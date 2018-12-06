<template>
    <div class="content_bg">
        <van-cell-group>
            <van-cell
                    :title="news_content.title"
                    :label="news_content.description"
                    title-class="title_class"
                    label-class="label_class"
            />
        </van-cell-group>
        <text>
            {{this.news_content.url}}
        </text>
        <button @tap="copy_url">复制原文地址</button>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                news_content: {
                    title: '',
                    description: '',
                    url: ''
                },
            }
        },
        onLoad(){
            console.log("正文页初始化");
            console.log(this.globalData.news_content);
            this.news_content = this.globalData.news_content;

            //设置标题。
            wx.setNavigationBarTitle({
                title: this.news_content.title
            })
        },
        methods: {
            copy_url(){
                wx.setClipboardData({
                    data: this.news_content.url,
                    success (res) {
                        wx.showToast({
                            title: '已复制',
                            icon: 'success',
                            duration: 2000
                        })
                    }
                })
            }
        },
    }
</script>

<style>
    .content_bg{
        margin-top: 10rpx;
    }
    .userinfo {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .userinfo-avatar {
        width: 128 rpx;
        height: 128 rpx;
        margin: 20 rpx;
        border-radius: 50%;
    }

    .userinfo-nickname {
        color: #aaa;
    }

    .usermotto {
        margin-top: 150px;
    }

    .form-control {
        display: block;
        padding: 0 12px;
        margin-bottom: 5px;
        border: 1px solid #ccc;
    }
    .title_class{
        font-size:40rpx;
        font-weight: bold;
    }
    .label_class{
        font-size: 40rpx!important;
        line-height: 60rpx!important;
        color: #7d7e80!important;
        padding-top: 30rpx;
        border-top: 1px solid #eee;
        margin-top: 30rpx;
        font-weight: normal;

    }

</style>
