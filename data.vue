 <!--日期选择插件(自写)-->
<template>
    <div class="screen-search change-date">
        <div class="screen">
            <span>日期</span>
            <ul class="screen-ul">
                <li style='width: 110px;height: 36px;' :class="[{'active':(menuIndex==index)}]" v-for="(data,index) in dataList" :key='index' @click='changeType(index,data)'><a href="#" :class="{'today':(today==data.date)}"><span>{{data.week}} </span><span>{{data.date}}</span></a></li>
            </ul>
        </div>
        <div class="search-group">
            <button class="btn btn-last-week" @click='lastWeek()'> 上一周 </button><span @click='toToday()' style="cursor: pointer;" class="toToday">{{today2}}</span><button class="btn btn-next-week"  @click='nextWeek()'>下一周 > </button>
        </div>
    </div>

</template>

<script>
import Vue from 'vue';

export default {
    data(){
        return {
            dataList:[],
            whichWeek:0,
            DayStemp:[],
            today2:new Date().getFullYear() + '/' + (new Date().getMonth() + 1) + '/' + new Date().getDate(),
            today: new Date().getFullYear() + '-' + (new Date().getMonth() + 1) + '-' + new Date().getDate(),
            menuIndex:0 
        }
    },
    created(){
        this.forEachData(this.whichWeek)
    },
    methods:{
        toToday(){
            this.whichWeek = 0
            this.menuIndex = 0 
            this.forEachData(this.whichWeek)
        },
        forEachData(whichWeek){
            let today = new Date().getTime()
            this.DayStemp = []
            for(var i = 1 + 7 * whichWeek;  i <= 7 + 7 * whichWeek;  i++) {
                this.DayStemp.push( new Date((24 * 60 * 60 * 1000) * (i-1) + today)) //1-7天的时间
            }
            this.setDate()
        },
        setDate(){
            // this.$set(vm.items, indexOfItem, newValue)
            //vue响应式原理 当直接通过某个键改变值 数据不会发生响应 所以要使用 this.$set()
            for(var i=1; i <= 7;  i++){
                this.$set(this.dataList,i-1,{'week':this.setWeek(this.DayStemp[i-1].getDay()),'date':this.DayStemp[i-1].getFullYear() + '-' + (this.DayStemp[i-1].getMonth() + 1) + '-' + this.DayStemp[i-1].getDate()})
            }
        },
        setWeek(week){
            switch(week){
                case 0:
                    return '星期日'
                    break
                case 1:
                    return '星期一'
                    break
                case 2:
                    return '星期二'
                    break
                case 3:
                    return '星期三'
                    break
                case 4:
                    return '星期四'
                    break
                case 5:
                    return '星期五'
                    break
                case 6:
                    return '星期六'
                    break
            }   
        },
        nextWeek(){
            this.whichWeek = this.whichWeek + 1
            this.forEachData(this.whichWeek)
            console.log(this.whichWeek)
        },
        lastWeek(){
            this.whichWeek = this.whichWeek - 1
            this.forEachData(this.whichWeek)
            console.log(this.whichWeek)
        },
        changeType(index,data){
            this.menuIndex = index
            console.log(new Date(data.date))
            //toUTCString()如何使用 toUTCString() 将当日的日期（根据 UTC）转换为字符串。 Fri, 14 Dec 2018 03:42:29 GMT
        }
      
    }
}
</script>
<style scoped lang="less" src="../pages/cygl/template.less"></style>
<style>
.today{background-color: #fd6666!important;color:white!important;}
.toToday{transition: all .2s;}
.toToday:hover{background-color: #fd6666!important;transition: all .2s;}
*{font-family: BMYH;}
.second-menu{background: white;overflow: hidden;width:100%;}
.second-menu>ul{margin-top:20px;height: 42px;line-height: 42px;margin-left:12px;}
.second-menu>ul>li{float:left;width:120px;text-align: center;cursor: pointer;background: white;margin: 0 8px;border-radius: 6px 6px 0 0;transition:all .3s;}
.second-menu>ul>li.active,.second-menu>ul>li:hover{background: #ebf1fe;transition:all .3s;}
.section{padding:15px 20px 0 20px;position: relative;height:90%;}
.screen-search{border-bottom:1px solid #77a6fe;padding-bottom:10px;margin-bottom:20px;overflow: hidden;}
.screen-search>.screen{float:left;line-height: 30px;}
.screen-search>.screen>span{margin:0 16px 0 30px;float:left;}
.screen-search>.screen>ul{float: left;}
.screen-search>.screen>ul>li{float: left;}
.screen-search>.screen>ul>li>a{display: block;padding:0 20px;border-radius: 20px;font-size: 14px;color: #333333;margin: 0 2px;transition:all .3s;}
.screen-search>.screen>ul>li.active>a,.screen-search>.screen>ul>li>a:hover{background-color:#77a6fe;color: white;transition:all .3s;}
.search-group{float: right;border:1px solid #77a6fe;line-height: 32px;border-radius: 20px;height: 32px;}
.search-group>.search-group-addon{background:#77a6fe;padding: 0 15px;display: inline-block;border-radius: 20px 0 0 20px;}
.search-group>#search{border:none;height: 30px;border-radius: 0 20px 20px 0;background: transparent;text-align: center;}
.cuisine>.cuisine-box{float: left;width: 20%;padding-right: 10px;padding-left: 10px;box-sizing: border-box;margin-bottom: 20px;}
.cuisine>.cuisine-box>.cuisine-item:hover{box-shadow:0 1px 30px rgba(119, 166, 254, 0.8);transition:all .3s;}
.cuisine>.cuisine-box>.cuisine-item{box-shadow: 0 0 2px 2px rgba(0,0,0,0.1);border-radius: 5px;transition:all .3s;}
.cuisine-item-top{position: relative;}
.cuisine-item-top>img{width:100%;}
.cuisine-item-top>.trade-name{position: absolute;bottom: 0;left:0;right:0;background: rgba(255,255,255,0.5);padding:5px 10px;text-overflow:ellipsis;overflow: hidden;white-space: nowrap;}
.cuisine-item-bottom{padding:6px 10px;font-size: 14px;color: #666666;}
.cuisine-item-bottom>.type-price{overflow: hidden;}
.cuisine-item-bottom>.type-price>span{display: block;}
.cuisine-item-bottom>.type-price>.type{width:82%;text-overflow: ellipsis;overflow: hidden;float:left;white-space: nowrap;}
.cuisine-item-bottom>.type-price>.price{color: #ff4f4f;font-size: 16px;float: right;}
.cuisine-item-bottom>.introduce{display: -webkit-box;-webkit-box-orient: vertical;-webkit-line-clamp: 2;overflow: hidden;line-height: 24px;margin-bottom:4px;}
.cuisine-item-bottom>.switch-div{text-align: right;}
.cuisine-item-bottom>.switch-div>.switch-wrap{display: inline-block;position: relative;}
.cuisine-item-bottom>.switch-div>span{color: #77a6fe;}
.cptj{display: block;position: relative;width:100%;}

.bottom-ope{position: absolute;bottom: 0px;right: 20px;background: white;height: 44px;line-height: 44px;padding:0 30px;box-sizing: border-box;box-shadow: 0 0 8px 1px rgba(0,0,0,0.1);left: 20px;}
.bottom-ope>.left-btn{float: left;}
// .bottom-ope>.left-btn>.allCheckbox{}
.bottom-ope>.left-btn>span{margin:0 20px;color:#77a6fe; }
.bottom-ope>.left-btn>.btn{width:80px;height: 26px;line-height: 26px;font-size: 15px;}
.bottom-ope>.left-btn>.btn-tjcp{background: #4053e4;}
.bottom-ope>.left-btn>.btn-cpdr{background: #77a6fe;}
.bottom-ope>.left-btn>.btn-tpdr{background: #ab9fff;}
.bottom-ope>.left-btn>.btn-sc{background: #ff4f4f;}
.bottom-ope>.paging{float: right;}
.bottom-ope>.paging>li{float: left;}
.bottom-ope>.paging>li>a{color:#77a6fe;padding:8px; }
.section2>.left{margin-right: 295px;}
.section2>.right{width:275px;float: right;height: 500px;}
.change-date>.screen{line-height: normal;}
.change-date>.screen>ul>li>a{border-radius: 4px;padding:2px 10px;}
.change-date ul>li>a>span{display: block;text-align: center;}
.change-date .search-group{ border-color: transparent;border-radius: 4px;}
.change-date .search-group>.btn{height: 100%;color: #b0aeae;border: 1px solid #b0aeae;padding: 0 10px;border-radius: 0;margin-top: 1px;transition:all .3s;}
.change-date .search-group>.btn:hover{border: 1px solid #77a6fe;color:#77a6fe;transition:all .3s;}
.change-date .search-group>span{display: inline-block;background: #77a6fe;color: white;padding: 0 30px;}
.change-date>.screen>span{line-height: 42px;}
.box-list{margin-left: -10px;margin-right: -10px;}
.box-list>.box-item{float: left;width: 140px;height:100px;padding-right: 10px;padding-left: 10px;box-sizing: border-box;margin-bottom:20px;}
.box-list>.box-item>.real-box{box-shadow: 0 0 2px 2px rgba(0,0,0,0.1);border-radius: 6px;cursor: pointer;}
.box-list>.box-item.active>.real-box{box-shadow: 0 0 2px 2px #77a6fe;}
.box-state>span{display: inline-block;width:59.5px;float: left;height: 38px;line-height: 38px;text-align: center;color: white;}
.box-state>span:first-child{border-top-left-radius: 6px;border-right:1px solid white;}
.box-state>span:last-child{border-top-right-radius: 6px;}
.state1{background-color: #ff6c6c;}
.state2{background-color: #ffbc6c;}
.state3{background-color: #97bbff;}
.box-name{height: 62px;line-height: 62px;text-align: center;}

.right>.right-top{background-color: #455471;padding:15px 10px;height: 184px;position: relative;}
.right>.right-top>.myxx{display: block;margin:10px auto;}
.right>.right-top>.myxx:first-child{margin-top:30px;}
.box-number{color: white;line-height: 26px;position: absolute;bottom: 15px;padding-left:5px;}
.bxzh{width: 135px;height: 26px;border-radius: 4px;border: none;margin-left: 15px;}
.bjxx{border-bottom:1px dashed white;color:white;padding:0 5px 10px 5px;}
.bjxx>p{line-height: 32px;text-overflow: ellipsis;overflow: hidden;white-space: nowrap;}
.right-list{background-color: white;padding:12px 10px;}
.right-list>.list-type>li{float: left;text-align: left;color: #666666;}
.right-list>.list-type>li:nth-child(1){width:60%;padding-left: 10px;box-sizing: border-box;}
.right-list>.list-type>li:nth-child(2){width:20%;text-align: center;}
.right-list>.list-type>li:nth-child(3){width:20%;text-align: center;}
.menu-detail-box{overflow-y:auto;margin-top:10px;}
.menu-detail-box>.menu-detail{line-height: 30px;}
.menu-detail-box>.menu-detail>div{display: inline-block;text-overflow: ellipsis;overflow: hidden;white-space: nowrap;text-align: left;}
.menu-detail-box>.menu-detail>div:nth-child(1){width:60%;}
.menu-detail-box>.menu-detail>div:nth-child(2){width:20%;text-align: center;}
.menu-detail-box>.menu-detail>div:nth-child(3){width:20%;text-align: center;}
.right-bottom{background-color: white;padding:10px 20px;margin-top:5px;}
.right-bottom>.sum>span{width:50%;float: left;}
.right-bottom>.sum>span:last-child{text-align: right;}
.right-bottom>.two-button{margin-top:9px;}
.right-bottom>.two-button>.btn{width:100px;background-color:#455471;height: 30px;line-height: 30px;}
.right-bottom>.two-button>.btn:last-child{float: right;}
</style>
