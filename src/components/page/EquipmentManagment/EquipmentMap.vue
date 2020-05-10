<template>
    <div>
         <baidu-map class="map" :center="map.center" :zoom="map.zoom" @ready="handler">
            <!--缩放-->
            <bm-navigation anchor="BMAP_ANCHOR_TOP_LEFT"></bm-navigation>
            <!--定位-->
            <bm-geolocation anchor="BMAP_ANCHOR_BOTTOM_RIGHT" :showAddressBar="true" :autoLocation="true"></bm-geolocation>
            <!--点-->
            <bm-marker v-for="point in map.points"  :key="point.name" :position="{lng: point.lng, lat: point.lat}" 
                @click="changeStatus(point)">
                <bm-info-window :show="point.showFlag" @close="close(point)">
                    {{point.name}}
                    <hr>
                    <p>经纬度:{{point.lng}},{{point.lat}}</p>
                    <p>可用充电桩:{{point.num}}</p>
                </bm-info-window>
            </bm-marker>
        </baidu-map>
    </div>
</template>
 
<script>
    export default {
        name: "demo",
        data: () =>({
            map:{
                center: {lng: 114.365818,lat:30.534872},
                points:[
                    {name:"富强印务店",lng:114.364175,lat:30.534118,showFlag:false,num:2},
                    {name:"德仁广场店",lng:114.365604,lat:30.53574,showFlag:false,num:0},
                    {name:"珞珈广场店",lng:114.367238,lat:30.54109,showFlag:false,num:3},
                    {name:"卓尔体育馆店",lng:114.363843,lat:30.543298,showFlag:false,num:1},
                    {name:"枫园一舍店",lng:114.377515,lat:30.544262,showFlag:false,num:2},
                    {name:"工学部网球场店",lng:114.370257,lat:30.547917,showFlag:false,num:2},
                    {name:"工学部8舍店",lng:114.370832,lat:30.550343,showFlag:false,num:2},
                ],
                zoom: 15,
                dragging: true
            }
        }),
        methods: {
            handler ({BMap, map}) {
                let me = this;
                //console.log(BMap, map)
                // 鼠标缩放
                map.enableScrollWheelZoom(true);
                // 点击事件获取经纬度
                map.addEventListener('click', function (e) {
                    console.log(e.point.lng, e.point.lat)
                })
            },
            // 点击标志，showFlag改为true
            changeStatus(point){
                for(var i = 0;i<this.map.points.length;i++){
                    if(this.map.points[i].name == point.name){
                        this.map.points[i].showFlag=true;
                        //console.log(this.map.points[i]);
                    }
                }
            },
            //点击说明，坐标的showFlag改为false
            close(point){
                for(var i = 0;i<this.map.points.length;i++){
                    if(this.map.points[i].name == point.name){
                        this.map.points[i].showFlag=false;
                        //console.log(this.map.points[i]);
                    }
                }
            }
        }
    }
    
</script>
 
<style scoped>
    .map {
        width: 100%;
        height: 500px;
    }
    .point {
        width: 30px;
        height: 30px;
    }
</style>