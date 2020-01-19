---
title: vue+uni-app开发天猫商城小程序案例
layout: article
sharing: true
license: true
aside:
  toc: true
show_edit_on_github: true
pageview: true
tags: 小程序
cover: "/assets/images/blog-images/VUE/天猫商城.webp"
key: 2019120905
---

今次利用HBuilderX和vue.js开发了一个天猫购物商城首页，供大家学习和参考。
底下附上代码和github下载连接。

先上效果图：

![](/assets/images/blog-images/VUE/天猫商城.webp)


开发天猫商城首页排版有两个重点，**文件的引入**和**v-for**的使用。
组件是视图层的基本组成单元，所以根节点为` <template>`，这个 `<template>` 下只能有一个根组件。我们整个天猫商城首页视图层都是在template标签完成。
现在来讲一下开发天猫商城首页的重点部分.




## 一、文件的引入

Vue文件的引入需要使用import 关键词。

![](/assets/images/blog-images/VUE/uni-app组件.png)

天猫商城例子我是用到uni-app组件，文件导入之后需要使用映入使用import 关键词引入到vue文件的js中。
例如：
```
import uniGrid from "@/components/uni-grid/uni-grid.vue"
import uniIcon from "@/components/uni-icon/uni-icon.vue"
export default {
        components: {uniIcon,uniGrid},
}
```


另外在项目里使用本地图片的时候，要引入图片到模版中。并且要给图片绑定变量。


例如：
Html部分：
```
<image class="main-img" :src="title.img" mode=""></image>
```

Js部分：
```
import img1 from "@/static/img-01.jpg"
import img2 from "@/static/img-02.jpg"
import img3 from "@/static/img-03.jpg"
import img4 from "@/static/img-04.jpg"

export default {
        
        
        data() {
            return {
                titles:[
                    {text:'限时抢购',img:img1},
                    {text:'天猫好物',img:img2},
                    {text:'聚划算',img:img3},
                    {text:'天猫闪购',img:img4}
                ]
}
}
}


```



## 二、v-for的使用

因为在实际开发项目时，很多都是格式一样，数据不一样，就想这个天猫商城首页的商品部分，排版格式都是一样的，只是图片标题和价格不一样，这时候我们可以使用v-for来便利数据，只需要在html模版部分添加样式和数据绑定的属性就可以。

例如：

```
// 猜你喜欢 
<view class="goods-content">
                <view class="goods-item" v-for='item in goods'>
                    <view class="img">
                        <image :src="item.img" mode=""></image>
                    </view>
                    <view class="goods-title">
                        {{item.title}}
                    </view>
                    <view class="footer">
                        <view class="price">
                            {{item.price}}
                        </view>
                        <view class="like">
                            看相似
                        </view>
                    </view>
                </view>
            </view>
```

在需要被遍历的元素的上一级，也就是父元素添加v-for属性，以便它的下一级都可以使用数组元素属性。

```
export default {
        data() {
            return {
                goods:[
                    {title:'迪士尼宝宝儿童帽潮薄款公主太阳帽',price:'￥52',img:goods1},
                    {title:'龙虎 清凉油 3g/盒 药品满88元包邮',price:'￥88',img:goods2},
                    {title:'风运动中长款修身连衣裙夏两件套装',price:'￥63',img:goods3},
                    {title:'华为荣耀v10/v20背夹充电宝9轻薄',price:'￥98',img:goods4}
                ]
}
}
}
```




## 三、附上项目的完整代码

```
<template>
     <view class="content" id="tmall">
         <!-- search -->
            <view class="uni-form-item uni-column header-search">
                <uni-icon class="search-icon" type="search" size="30"></uni-icon>
             <input class="uni-input header-input" confirm-type="search" placeholder="落地风扇" />
            </view>
            
            <!-- menu -->       
            <uni-grid :options="menu" column-num="5" show-border="false">
            </uni-grid>
            
            <!-- swiper -->
            <view class="uni-padding-wrap">
                <view class="page-section swiper">
                    <view class="page-section-spacing">
                        <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
                            <swiper-item>
                                <view class="swiper-item">
                                    <image class='img-ad' src="//gw.alicdn.com/tps/i4/TB1ZgvOSxTpK1RjSZFMSuvG_VXa.jpg_790x10000Q75.jpg_.webp" mode=""></image>
                                </view>
                            </swiper-item>
                            <swiper-item>
                                <view class="swiper-item">
                                        <image class='img-ad' src="//gw.alicdn.com/tfs/TB1h3OGShjaK1RjSZFAXXbdLFXa-1035-390.jpg_790x10000Q75.jpg_.webp" mode=""></image>
                                </view>
                            </swiper-item>
                            <swiper-item>
                                <view class="swiper-item">
                                        <image class='img-ad' src="//gw.alicdn.com/imgextra/i2/26/O1CN01jrwKAz1C3woePAzH5_!!26-0-lubanu.jpg_790x10000Q75.jpg_.webp" mode=""></image>
                                </view>
                            </swiper-item>
                        </swiper>
                    </view>
                </view>
            </view>
        
            <!-- 优惠 -->
            <view class="main">
                <view class="main-item" v-for="title in titles">
                    <view>
                        <view class="title">{{title.text}}</view>
                    </view>
                    <view>
                        <image class="main-img" :src="title.img" mode=""></image>
                    </view>
                </view>
            </view>
            
            <!-- 热销单品 -->
            <view class="hot">
                <view class="hot-item hot_A" v-for="item in hottitle">
                    <view class="hot_title">
                        <view>{{item.titlea}}</view>
                        <view>{{item.titleb}}</view>
                        <view>{{item.titlec}}</view>
                    </view>
                    <image :src="item.image" mode=""></image>
                </view>
                
                <view class="hot-item" v-for="item in hots">
                    <view class="hot_title">
                        <view>{{item.titlea}}</view>
                        <view>{{item.titleb}}</view>
                        <view>{{item.titlec}}</view>
                    </view>
                    <image class="hot-img" :src="item.image" mode=""></image>
                </view>
            </view>
                    
            
            <!-- 猜你喜欢 -->
            <view class="goods-content">
                <view class="goods-item" v-for='item in goods'>
                    <view class="img">
                        <image :src="item.img" mode=""></image>
                    </view>
                    <view class="goods-title">
                        {{item.title}}
                    </view>
                    <view class="footer">
                        <view class="price">
                            {{item.price}}
                        </view>
                        <view class="like">
                            看相似
                        </view>
                    </view>
                </view>
            </view>
            
     </view>
</template>

<script>
    
    import uniGrid from "@/components/uni-grid/uni-grid.vue"
    import uniIcon from "@/components/uni-icon/uni-icon.vue"
    
    import img1 from "@/static/img-01.jpg"
    import img2 from "@/static/img-02.jpg"
    import img3 from "@/static/img-03.jpg"
    import img4 from "@/static/img-04.jpg"
    
    import goods1 from "@/static/goods-01.webp.jpg"
    import goods2 from "@/static/goods-02.webp.jpg"
    import goods3 from "@/static/goods-03.webp.jpg"
    import goods4 from "@/static/goods-04.webp.jpg"
    

    export default {
        
        components: {uniIcon,uniGrid},
        data() {
            return {
                goods:[
                    {title:'迪士尼宝宝儿童帽潮薄款公主太阳帽',price:'￥52',img:goods1},
                    {title:'龙虎 清凉油 3g/盒 药品满88元包邮',price:'￥88',img:goods2},
                    {title:'风运动中长款修身连衣裙夏两件套装',price:'￥63',img:goods3},
                    {title:'华为荣耀v10/v20背夹充电宝9轻薄',price:'￥98',img:goods4}
                ],
                
                titles:[
                    {text:'限时抢购',img:img1},
                    {text:'天猫好物',img:img2},
                    {text:'聚划算',img:img3},
                    {text:'天猫闪购',img:img4}
                ],
                
                hots:[
                    {titlea:'人气榜',titleb:'品质优雅单鞋榜',titlec:'月销量22万',image:img1},
                    {titlea:'人气榜',titleb:'潮流时尚卫衣榜',titlec:'月销量22万',image:img3},
                    {titlea:'人气榜',titleb:'品质优雅单鞋榜',titlec:'月销量22万',image:img4},
                    {titlea:'人气榜',titleb:'潮流时尚卫衣榜',titlec:'月销量22万',image:img1}
            
                ],
                
                hottitle:[
                    {titlea:'人气榜',titleb:'潮流时尚卫衣榜',titlec:'月销量22万',image:img1},
                ],
            
                menu:[
                    {image:'//gw.alicdn.com/tfs/TB1ISdWSFXXXXbFXXXXXXXXXXXX-146-147.png_110x10000.jpg_.webp',text:'圣诞树'},
                    {image:'//gw.alicdn.com/tfs/TB1wSoFa5qAXuNjy1XdXXaYcVXa-196-196.png?avatar=1_110x10000.jpg_.webp',text:'铃铛'},
                    {image:'//gw.alicdn.com/tfs/TB1Jc0fSFXXXXXTapXXXXXXXXXX-146-147.png_110x10000.jpg_.webp',text:'圣诞老人'},
                    {image:'//gw.alicdn.com/tfs/TB15lhOSFXXXXaKXpXXXXXXXXXX-147-147.png_110x10000.jpg_.webp',text:'礼物'},
                    {image:'//gw.alicdn.com/tfs/TB12CFXSFXXXXcpapXXXXXXXXXX-146-147.png_110x10000.jpg_.webp',text:'帽子'}
                    ],
                    indicatorDots: true,
                    autoplay: true,
                    interval: 2000,
                    duration: 500,
            }
        },
        onLoad() {
        },
        methods: {
        changeIndicatorDots(e) {
this.indicatorDots = !this.indicatorDots
},
changeAutoplay(e) {
this.autoplay = !this.autoplay
},
intervalChange(e) {
this.interval = e.target.value
},
durationChange(e) {
this.duration = e.target.value
}
        }
    }
</script>

<style>
    body{
        background-color: #F1F1F1;
    }
        
    .header-search{
            background-color: rgb(255, 0, 54);
            padding: 6px;
        }
        
        .header-search .header-input{
            padding: 6px;
            background-color: #ffffff;
            border-radius: 5px;
            padding-left: 30px;
        }
        
        .header-search .search-icon{
            position: absolute;
            color: #C8C7CC;
        }
        
        .swiper{
            height: 120px;
        }
        
        .page-section.swiper{
            padding: 0 10px;
            
        }
        
        .img-ad{
            height: 120px;
            width: 100%;
        }
        
        .main{
            padding: 20px 10px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-row-gap: 8px;
            grid-column-gap: 8px;
            grid-auto-rows: 150px; 
        }
        
        .main-item{
            border-radius: 5px;
            overflow: hidden;
        }
        
        .main-item .title{
            font-size: 18px;
            font-weight: 600;
            padding-left: 10px;
            padding-top: 10px;
            position: absolute;
            z-index: 99;
        }
        
        .hot{
            display: grid; 
            grid-template-columns: repeat(2, 1fr); 
            grid-auto-rows: 80px; 
            grid-row-gap: 8px;
            grid-column-gap: 8px;
            padding: 0 10px;
        }
        
        .hot .hot-item{
            background-color: #C8C7CC;
            overflow: hidden;
            
        }
        
        .hot .hot-item .hot_title{
            font-size: 12px;
            position: absolute;
            padding-top:20px;
            padding-left:10px;
            
        }
        
        .hot .hot-item >*{
            width: 100%;
            height: auto;
        }
        
        
        .hot .hot_A{
             grid-column-start: 1;
             grid-column-end: 3;
        }
        
        .goods-content{
            padding: 20px 10px;
            display: grid;
            grid-template-columns: repeat(2, 1fr); 
            grid-row-gap: 8px;
            grid-column-gap: 8px;
            
        }
        
        .goods-content .goods-item{
            display: flex;
            flex-direction: column;
            background-color: #FFFFFF;
            overflow: hidden;
        }
        
        .goods-content .img{
            padding: 10px;
            overflow: hidden;
            height: 120px;
        }
        
        .goods-content .goods-item .goods-title{
            padding: 10px;
            font-size: 14px;
            color: #333333;
        }
        
        .goods-content .goods-item .footer{
            padding: 10px;
            display: flex;
            justify-content: space-between;
            
        }
        .goods-content .goods-item .footer .price{
            color: rgb(255, 0, 0);
            font-weight: 600;
        }
        
        
        .goods-content .goods-item .footer .like{
            padding: 3px 5px;
            border: 10px;
            background-color: rgb(255, 230, 235);
            color: rgb(255, 0, 0);
            border-radius: 10px;
            font-size: 14px;
        }
</style>
```

## 四、github连接

https://github.com/muimui2/tmall

推荐阅读：

[vue微信小程序图标引入——已解决](https://muitlog.com/2019/11/25/vue%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%9B%BE%E6%A0%87%E5%BC%95%E5%85%A5-%E5%B7%B2%E8%A7%A3%E5%86%B3.html)


[微信小程序动态修改页面标题](https://muitlog.com/2019/12/01/%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%8A%A8%E6%80%81%E4%BF%AE%E6%94%B9%E9%A1%B5%E9%9D%A2%E6%A0%87%E9%A2%98.html)