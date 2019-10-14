<template>
    <div class="box">
        <classify :arr="idArray"></classify>
        <div class="markdown-body">
            <h1>我的</h1>
            <label for="image" class="updata">
                <span>点击上传</span>
                <input style="display:none" type="file" name="image" id='image' @change="updata($event)" accept="image/*" />
            </label>
            <img :src="uri" alt="">
            <div>
                <span>Test</span>
                <span v-html="html"></span>
            </div>
        </div>

    </div>
</template>
<script>
    import Classify from '../../components/common/classify.vue'
    export default {
        components:{
            Classify
        },
        data(){
            return {
                idArray:[
                    {name:'我的'}
                ],
                uri:'',
                html:'<button style="padding:5px 15px" ref="test" id="test">click</button>'
            }
        },
        mounted(){
            console.log(this.$refs)
            this.$nextTick(function(){
                let test = document.getElementById('test');
                test.addEventListener('click',function(){
                    console.log(1111);
                })
            })
        },
        methods:{
            updata(e){
                let self = this;
                const image = e.target.files[0];
                var render = new FileReader();
                render.readAsDataURL(image);
                render.onload = function(e){
                    var result = this.result
                    console.log(result);
                    self.uri = result; 
                }
                
            },
            test(){
                console.log('哈哈哈')
            }
        }
    }
    
</script>
<style scoped lang="less">
    @media (max-width: 767px) {
         .box{
            padding: 15px 15px 0 15px;
        }
    }
    .updata{
        display: block;
        height: 35px;
        width: 120px;
        background-color:rgb(19, 80, 60);
        line-height: 35px;
        text-align: center;
        color: wheat;
    }




    /* screen-md-min & screen-md-max */
    @media (min-width: 768px) {
        .box{
            margin: 50px 0 0 50px;
        }
    }
</style>
