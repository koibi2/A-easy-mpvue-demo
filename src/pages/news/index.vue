<template>
    <div class="">
        <van-cell-group>
            <van-cell
                    v-if="value.title!==''"
                    v-for="(value,key) in news_list"
                    :key="key"
                    :title="value.title"
                    title-class="title_class"
                    @tap="jump_content(key)"
            />
        </van-cell-group>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                news_id: '',
                news_list: [],
            }
        },
        onLoad(e){
            this.news_id = e.news_id;
            let url = "http://localhost:3001/api/daily_info/" + this.news_id;
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
                        //设置标题。
                        wx.setNavigationBarTitle({
                            title: res.data.data.title
                        })
                        this.news_list = res.data.data.links;
                    }
                },fail (e){
                    console.log(e.errMsg);
                }
            })
        },
        methods: {
            jump_content(index){
                console.log("index："+index);
                console.log("this.news_list[index];"+this.news_list[index]);
                console.log("描述："+this.news_list[index].description);
                this.globalData.news_content = this.news_list[index];
                console.log("NEWS页已储存" + this.globalData.news_content);
                wx.navigateTo({
                    url :"../content/main"
                })
            }
        },
    }
</script>

<style scoped>
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
        /*background-color: red!important;*/
        /*color: red!important;*/
        color: red;
         display: -webkit-box;
        word-break: break-all;
        text-overflow: ellipsis;
        overflow: hidden;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 1;
    }

</style>
