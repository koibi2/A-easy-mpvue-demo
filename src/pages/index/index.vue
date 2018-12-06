<template>
    <div class="">
        <van-cell-group>
            <van-cell
                    v-for="(value,key) in news"
                    :key="key"
                    :title="value.title"
                    :label="value.description"
                    label-class="label_class"
                    @tap="jump_news(value.id)"
            />
        </van-cell-group>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                motto: 'Hello World',
                userInfo: {},
                news: [],
            }
        },
        methods: {
            jump_news(news_id){
                wx.navigateTo({
                    url: '../news/main?news_id=' + news_id
                })
            }
        },
        onLoad() {
            let url = "http://localhost:3001/api/daily_list";
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
                    console.log(typeof (res.data.code));
                    if(res.data.code === 200){
                        console.log("AJAX成功");
                        this.news = res.data.data;
                    }
                },fail (e){
                    console.log(e.errMsg);
                }
            })
        }
    }
</script>

<style>
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
    .label_class{
        /*background-color: red!important;*/
        /*color: red!important;*/
        color: red;
         display: -webkit-box;
        word-break: break-all;
        text-overflow: ellipsis;
        overflow: hidden;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 3;
    }
    .custom-class{

        background-color: red;
        color: red;
    }
</style>
