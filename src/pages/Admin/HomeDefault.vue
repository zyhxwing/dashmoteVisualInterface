<template>
	<div class="bar">
    <div class="leftBar"></div>
    <div class="centerBar">
      <div class="topToolBar">
        <a-input-search placeholder="Search for a keyword"   class ="search" @search="onSearch" >
        </a-input-search>
      </div>

      <div class="userName">{{'Hello '+userName +'!'}}
        </div>
      <div class="text">Here you can find your projects and dashboards.</div>
      <div class="searchBar">
        <a-input-search placeholder="Search"   class ="search" @search="onSearch" >
        </a-input-search>
      </div>
      <a-list
        class="demo-loadmore-list"
        item-layout="horizontal"
        :data-source="tbMainData"
      >
        <a-list-item slot="renderItem" slot-scope="item, index" @click="openDetail(item)">
          <a slot="actions" class="deleteButton" @click="deleteItem(item,index)"  onClick="event.cancelBubble = true">Delete</a>
          <div class="colorBlock" :style="{background:colorList[index%3]}"></div>
          <div class="avatarAndContent">
            <a-avatar :style="{background:avatarColorList[index%3],color:colorList[index%3]}"
                      style="margin-left:10px;font-weight: bold">{{ item.type }}</a-avatar>
            <div  class="contentName" >{{ item.name }}</div>
          </div>
          <div class="content">{{ item.users+' users' }}</div>
          <div class="dashboards">{{ item.dashboards+' dashboards' }}</div>
        </a-list-item>
      </a-list>

      <a-modal
        title="详情"
        width="300px"
        :visible="visible"
        @ok="handleOk"
        @cancel="handleCancel"
      >
        <div class="modalStyle">
          <div class="modalItem">
            <p>name</p>  <p>{{ detail.name }}</p>
          </div>
          <div  class="modalItem">
            <p>users</p> <p>{{ detail.users }}</p>
          </div>
          <div  class="modalItem">
            <p>dashboards</p> <p>{{ detail.dashboards }}</p>
          </div>
          <div  class="modalItem">
            <p>type</p> <p>{{ detail.type }}</p>
          </div>
        </div>
      </a-modal>

    </div>
      <div class="rightBar"></div>
	</div>
</template>

<script>
import { message, Modal } from "ant-design-vue";
	export default{
		data(){
			return{
        userName:"Sarah",
        colorList:['#24AE5C', '#B37FEB','#1990FF'],
        avatarColorList:['#CCF5E3', '#F0E5FB','#D1E9FF'],
        tbMainData: [],
        storeData: [],
        detail:{},
        visible: false,
			}
		},
		mounted() {
      this.getData();
		},
		methods:{
      openDetail(item){
        this.visible = true;
        this.detail = item;
      },
      handleOk(e) {
        this.visible = false;
      },
      handleCancel(e) {
        this.visible = false;
      },
      deleteItem(row,index){
        Modal.confirm({
          centered: true,
          title: "是否确认删除",
          onOk: () => {
            console.dir(row)
            console.dir(index)
            let newArray=this.storeData.filter(function (element, order) {
              return order!=index
            });
            this.tbMainData = newArray
            this.storeData = newArray
            message.info("数据已删除");
          },
        });
      },
      onSearch(input){
        let newArray=this.storeData.filter(x=>{
          return x.name.indexOf(input)!=-1
        })
        this.tbMainData= newArray
      },
      getData() {
        this.tbMainData = [
          {
          name: 'Project A',
          dashboards:3,
          users:3,
          type:'C',
          },
          {
            name: 'Project B',
            dashboards:3,
            users:1,
            type:'F',
          },
          {
            name: 'Project C',
            dashboards:4,
            users:2,
            type:'D',
          },
          {
            name: 'Project D',
            dashboards:3,
            users:4,
            type:'C',
          },
        ]
        this.storeData = this.tbMainData
      },
		}
	}
</script>

<style lang="scss" scoped>
.bar{
  display: flex;
  border-top: 1px solid #C4C4C4;
}
.leftBar{
  width:136px
}
.rightBar{
  width:136px
}
.centerBar{
  flex:1;
}
.topToolBar{
  margin-top: 136px;
  display: flex;
  justify-content: flex-end
}
.userName{
  width: 137px;
  margin-left: 24px;
  height: 38px;
  font-family: Roboto;
  font-style: normal;
  font-weight: 700;
  font-size: 24px;
  line-height: 38px;
  letter-spacing: 0.02em;
  color: #223273;
  display: none;
  justify-content: center
}
.text{
  width: 339px;
  height: 20px;
  font-family: 'Roboto Light';
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.02em;
  color: #223273;
  margin-left: 24px;
  display: none;
  justify-content: center
}
.searchBar{
  margin-top: 50px;
  display: none;
  justify-content: center
}
.search{
  width: 222px;
  height: 40px;
  margin-right: 10px;
}
.colorBlock{
  width: 10.5px;
  height:70px;
  border-radius: 4px 0px 0px 4px;
}
.deleteButton{
  color: #DD1155;
  font-family: Roboto;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 22px;
  margin-right: 50px;
}
.avatarAndContent{
  display: flex;
  align-items: center;
  width: 800px;
}
.content{
  font-family: Roboto;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 22px;
  width: 117px;
  height: 22px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.contentName{
  font-weight: bold;
  margin-left: 10px;
  font-family: Roboto;
  font-style: normal;
  font-size: 14px;
  line-height: 22px;
  width: 117px;
  height: 22px;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.dashboards{
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 4px 16px;
  gap: 10px;
  width: 127px;
  height: 22px;
  background: #CCF5E3;
  border: 1px solid #00CC74;
  border-radius: 4px;
  font-family: Roboto;
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 14px;
  color: #00CC74;
}
/deep/.ant-list-item{
  margin-right: 10px;
  background: #FFFFFF;
  height: 70px;
  margin-top: 10px;
  box-shadow: 0px 4px 20px rgba(120, 120, 120, 0.15);
  border-radius: 8px;
}
/deep/.ant-input-affix-wrapper .ant-input-suffix{
  left:12px;
  top: 45%;
  font-size: 16px;
}
/deep/.ant-input-affix-wrapper .ant-input:not(:last-child) {
  padding-left: 40px;
}
.demo-loadmore-list{
  height:100%;
  overflow: scroll;
}
// 滚动条
.demo-loadmore-list::-webkit-scrollbar {/*滚动条整体样式*/
  width: 8px;     /*高宽分别对应横竖滚动条的尺寸*/
  height: 1px;
}
.demo-loadmore-list::-webkit-scrollbar-thumb {/*滚动条里面小方块*/
  background: #C4C4C4;
  border-radius: 4px;
}
.demo-loadmore-list::-webkit-scrollbar-track {/*滚动条里面轨道*/
  -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
  background: #F1F1F1;
  border-radius: 4px;
}
.modalItem{
  display: flex;
  justify-content: space-between;
}
.modalStyle{
  display: flex;
  flex-direction: column
}
	.moduleAll{
		.onePart{
			width:25%;
			height: 100%;
			text-align:center;
			.cardMeta{
				display: flex;
				align-items: center;
				justify-content: center;
			}
		}
	}

@media only screen and (max-width: 400px) {
  .bar{
    display: flex;
    border-top: 0px solid #C4C4C4;
  }
  .leftBar{
    width:0px
  }
  .rightBar{
    width:0px
  }
  .centerBar{
    flex:1;
  }
  .userName{
    width: 153px;
    margin-left: 24px;
    height: 38px;
    font-family: Roboto;
    font-style: normal;
    font-weight: 700;
    font-size: 24px;
    line-height: 38px;
    letter-spacing: 0.02em;
    color: #223273;
    display: flex;
    justify-content: center
  }
  .text{
    width: 339px;
    height: 20px;
    font-family: 'Roboto Light';
    font-size: 14px;
    line-height: 20px;
    letter-spacing: 0.02em;
    color: #223273;
    margin-left: 24px;
    display: flex;
    justify-content: center
  }
  .searchBar{
    margin-top: 16px;
    display: flex;
    justify-content: center;
    margin-bottom:51px
  }
  .topToolBar{
    display: none!important;
    margin-top: 0px;
    justify-content: center
  }
  .search{
    width: 320px;
    height: 40px;
    margin-right: 10px;
  }
  .colorBlock{
    width: 10.5px;
    height:70px;
    border-radius: 4px 0px 0px 4px;
  }
  .deleteButton{
    display: none;
    color: #DD1155;
    font-family: Roboto;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 22px;
    margin-right: 50px;
  }
  .avatarAndContent{
    display: flex;
    align-items: center;
    width: 300px;
  }
  .contentName{
    font-family: Roboto;
    font-style: normal;
    font-weight: bold;
    margin-left: 33px;
    font-size: 14px;
    line-height: 22px;
    width: 117px;
    height: 22px;
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .content{
    display: none;
    font-family: Roboto;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 22px;
    width: 117px;
    height: 22px;
    flex-direction: row;
    align-items: center;
  }
  .dashboards{
    display: none;
    flex-direction: row;
    align-items: center;
    padding: 4px 16px;
    gap: 10px;
    width: 127px;
    height: 22px;
    background: #CCF5E3;
    border: 1px solid #00CC74;
    border-radius: 4px;
    font-family: Roboto;
    font-style: normal;
    font-weight: 400;
    font-size: 14px;
    line-height: 14px;
    color: #00CC74;
  }
  /deep/.ant-list-item{
    padding: 0;
    margin-left: 24px;
    margin-right: 24px;
    background: #FFFFFF;
    height: 70px;
    margin-top: 10px;
    box-shadow: 0px 4px 20px rgba(120, 120, 120, 0.15);
    border-radius: 8px;
  }
  /deep/.ant-input-affix-wrapper .ant-input-suffix{
    left:90%;
    top: 45%;
    font-size: 16px;
  }
  /deep/.ant-input-affix-wrapper .ant-input:not(:last-child) {
    padding-left: 5px;
    background-color: #f2f6fc;
    border: 0px ;
    border-radius: 0px;
    border-bottom: 1px solid #787878;
  }
  .demo-loadmore-list{
    height: 100%;
    overflow:unset;
  }
  // 滚动条
  .demo-loadmore-list::-webkit-scrollbar {/*滚动条整体样式*/
    width: 8px;     /*高宽分别对应横竖滚动条的尺寸*/
    height: 1px;
  }
  .demo-loadmore-list::-webkit-scrollbar-thumb {/*滚动条里面小方块*/
    background: #C4C4C4;
    border-radius: 4px;
  }
  .demo-loadmore-list::-webkit-scrollbar-track {/*滚动条里面轨道*/
    -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
    background: #F1F1F1;
    border-radius: 4px;
  }
  .modalItem{
    display: flex;
    justify-content: space-between;
  }
  .modalStyle{
    display: flex;
    flex-direction: column
  }
  .moduleAll{
    .onePart{
      width:25%;
      height: 100%;
      text-align:center;
      .cardMeta{
        display: flex;
        align-items: center;
        justify-content: center;
      }
    }
  }

}
</style>
