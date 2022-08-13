<template>
	<a-layout class="pageAll">
		  <a-layout-header class="pageHead">
        <img class="tableMenu"  :src="menu" />
        <img class="tableImg"  :src="icon" />
        <span class="titleText" >{{titleText}}</span>
        <img class="headPortraitImg"  :src="headPortrait" />
		  </a-layout-header>

		  <a-layout-content class="pageCont">
			  <a-spin  tip="Loading..." :spinning="loading" >
				  <router-view class="moduleAll"  />
			  </a-spin>
		  </a-layout-content>
	  </a-layout>
</template>

<script>
  import iconUrl from "./../assets/icon.png"
  import headPortraitUrl from "./../assets/Ellipse 2.png"
  import menuUrl from "./../assets/menu.png"
	export default {
		data(){
			return{
        titleText:"Sarah Green",
        icon:iconUrl,
        menu:menuUrl,
        headPortrait:headPortraitUrl,
				loading:true,
			}
		},
		mounted() {
			setTimeout(()=>{//加载。。。
				this.loading=false
			},500)
		},
		methods: {
		},
	}
</script>

<style lang="scss" scoped>

	.pageAll{
		width: 100vw;
		height:100vh;
		.pageHead{
      background: #f2f6fc;
			padding: 0 ;
			display: flex;
			align-items: center;
      justify-content: flex-end;
			.tableImg {
        width: 15px;
        height: 17px;
        margin-right: 32px;
			}
      .tableMenu{
        display: none;
      }
			.headPortraitImg{
        margin-right: 136px;
      }
      .titleText{
        width: 100px;
        height: 22px;
        font-family:Roboto Medium;
        font-size: 14px;
        font-weight: bold;
        line-height: 22px;
        color: #223273;
      }
		}

		.pageCont{
			overflow: hidden;
			height: 100%;
			.pgTab/deep/{
				.ant-tabs-bar{
					margin: 0;
				}
				/deep/.ant-tabs-card-bar,.ant-tabs-tab{
					height: 26px;
					line-height: 26px;
					font-size: 12px;
				}
			}
			.moduleAll{
				width: 100%;
      background-color: #f2f6fc;
      height: calc(100vh - 64px );
      &.hasTab{

        height: calc(100vh - 64px);
      }
    }
		}

	}

  @media only screen and (max-width: 667px) {
    .pageAll {
      width: 100vw;
      height: 100vh;
      /* For mobile phones: */
      .pageHead {
        background: #f2f6fc;
        padding: 0;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        .tableMenu{
          width: 18px;
          height: 14px;
          margin-right: 0px;
          position: absolute;
          left: 24px;
          display: inline-block;
        }
        .tableImg {
          width: 15px;
          height: 17px;
          margin-right: 0px;
        }
        .headPortraitImg {
          margin-right: 0px;
          margin-top: 10px;
        }
        .titleText {
          display: none;
          width: 100px;
          height: 22px;
          font-family: Roboto Medium;
          font-size: 14px;
          font-weight: bold;
          line-height: 22px;
          color: #223273;
        }
      }
    }

  }
</style>
