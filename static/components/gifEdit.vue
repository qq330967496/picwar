<template>
    <div id="gifEdit">

        <!--{{msg}}-->
        <div class="canvas_mod">
            <canvas id="myCanvas">
                Your browser does not support the HTML5 canvas tag.
            </canvas>
        </div>

        <div class="mod">
            <div>
                选择你的头：
            </div>

            <div class="img_list">
                <div class="img_list_item" v-for="(item,index) in data">
                    <img @click="changeImg(item,$event)" :src="item.img"  :class="{actived:index==0?true:false}"/>
                </div>
            </div>
        </div>
        <div class="mod">
            <div>
                选择你的节操：
            </div>
            <div>
                <input type='text' v-model='text_1'/>
                <input type="range" step="1" min="10" max="40" v-model="text_1_fontSize">{{text_1_fontSize}}px
            </div>
            <div>
                <input type='text' v-model='text_2'/>
                <input type="range" step="1" min="10" max="40" v-model="text_2_fontSize">{{text_2_fontSize}}px
            </div>
            <div class="text_list">
                <div @click="changeText" class="text_list_item" v-for="(item,index) in text_list" :class="{actived:index==0?true:false}">
                    <div class="text1">
                        {{item.text1}}
                    </div>
                    <div class="text2">
                        {{item.text2}}
                    </div>
                </div>
            </div>
        </div>


    </div>
</template>



<script>

    import utils from 'utils';

    export default{
        data(){
            return {
                msg:'',
                img_url:'',
                text_1:'屌爆了',
                text_1_fontSize:30,
                text_2:'JJ boom',
                text_2_fontSize:25,
                bg_color:'#fff',
                data:[
                    {id:'gif_1',name:'吹头发',img:'../images/gif_1.gif',bg_color:'#fff'},
                    {id:'gif_2',name:'吹头发2',img:'../images/gif_2.gif',bg_color:'#fff'},
                ],
                text_list:[
                    {text1:'屌爆了',text2:'JJ boom'},
                    {text1:'扑街',text2:'poor guy'},
                    {text1:'哈哈哈哈',text2:'23333333'},
                    {text1:'你坏坏',text2:'you bad bad'},
                    {text1:'因崔斯汀',text2:'interesting'},
                    {text1:'你们够了',text2:'You Enough'},
                    {text1:'辣鸡',text2:'Hot Chicken'},
                ]
            }
        },
        beforeCreate: function () {
            utils.adaptive();
        },
        updated:function(){
            this.init();
        },
        mounted: function () {
            var _self = this;
            _self.img_url = _self.data[0].img;
            _self.init();
        },
        methods: {
            init:function(){
                var _self = this;
                $("#img").remove();
                var $img = $('<img src="" alt="img" id="img" style="display:none;"/>');
                $img.attr('src',_self.img_url);
                $("#home").append($img[0]);
                $img[0].onload = function(){

//                    console.log($img[0].width+' X '+$img[0].height);

                    //设置画板
                    var c = $('#myCanvas')[0];
                    c.width = $img[0].width;
                    c.height = $img[0].height+Number(_self.text_1_fontSize)+Number(_self.text_2_fontSize)+15;
                    var ctx = c.getContext("2d");

                    //插入背景
                    ctx.fillStyle = _self.bg_color;
                    ctx.fillRect(0,0,c.width,c.height);

                    //插入图片
                    ctx.drawImage($img[0],0,0);

                    //设置字体样式
                    ctx.font = "bold "+_self.text_1_fontSize+"px 微软雅黑";
                    //设置字体填充颜色
                    ctx.fillStyle = "black";
                    //绘制文字
                    ctx.textAlign="center";
                    ctx.fillText(_self.text_1, $img[0].width/2, $img[0].height+Number(_self.text_1_fontSize));

                    ctx.font = "bold "+_self.text_2_fontSize+"px 微软雅黑";
                    ctx.fillText(_self.text_2, $img[0].width/2, $img[0].height+Number(_self.text_1_fontSize)+Number(_self.text_2_fontSize)+5);
                };
            },
            changeImg:function(item,event){
                var _self = this;
                _self.img_url = item.img;
                _self.bg_color = item.bg_color;
                _self.init();

                var $this = $(event.target);
                $(".img_list").find("img").removeClass("actived");
                $this.addClass("actived");


            },
            changeText:function(event){
                var $this = $(event.target).hasClass('text_list_item')?$(event.target):$(event.target).parents('.text_list_item');
                $(".text_list_item").removeClass("actived");
                $this.addClass("actived");
                this.text_1 = String.trim($this.find(".text1").html());
                this.text_2 = String.trim($this.find(".text2").html());
            }
        }
    }
</script>