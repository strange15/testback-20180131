<template>
  <div id="app">
    <div class="layout">
      <Layout>
        <Sider ref="side1">
          <div style="cursor: pointer;">
            <img src="http://lorempixel.com/400/200/" style="width:200px; height:80px;" alt="">
          </div>
          <Menu active-name="1-1" theme="dark" width="auto" :class="menuitemClasses" @on-select="naviSelect">
            <MenuItem name="1-1">
            <span>首頁</span>
            </MenuItem>
            <MenuItem name="1-2" href="/page">
            <span>未平倉單</span>
            </MenuItem>
            <MenuItem name="1-3">
            <span>已平倉單</span>
            </MenuItem>
            <MenuItem name="1-4">
            <span>入金紀錄</span>
            </MenuItem>
            <MenuItem name="1-5">
            <span>出金紀錄</span>
            </MenuItem>
            <MenuItem name="1-6">
            <span>邀請方式</span>
            </MenuItem>
            <MenuItem name="1-7">
            <span>轉帳紀錄</span>
            </MenuItem>
          </Menu>
        </Sider>
        <Layout>
          <Header :style="{padding: 0}" class="layout-header-bar">
            <div class="header">
              <div class="headerLeft">
                <div>
                  <div class="avatar">
                    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFAAAABQCAYAAAH5FsI7AAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyFpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNS1jMDE0IDc5LjE1MTQ4MSwgMjAxMy8wMy8xMy0xMjowOToxNSAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvIiB4bWxuczp4bXBNTT0iaHR0cDovL25zLmFkb2JlLmNvbS94YXAvMS4wL21tLyIgeG1sbnM6c3RSZWY9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9zVHlwZS9SZXNvdXJjZVJlZiMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIChXaW5kb3dzKSIgeG1wTU06SW5zdGFuY2VJRD0ieG1wLmlpZDo5NDc2Q0YwMTkxRUUxMUU3OUZBMkFEREMyNzRDOTlCOSIgeG1wTU06RG9jdW1lbnRJRD0ieG1wLmRpZDo5NDc2Q0YwMjkxRUUxMUU3OUZBMkFEREMyNzRDOTlCOSI+IDx4bXBNTTpEZXJpdmVkRnJvbSBzdFJlZjppbnN0YW5jZUlEPSJ4bXAuaWlkOjk0NzZDRUZGOTFFRTExRTc5RkEyQUREQzI3NEM5OUI5IiBzdFJlZjpkb2N1bWVudElEPSJ4bXAuZGlkOjk0NzZDRjAwOTFFRTExRTc5RkEyQUREQzI3NEM5OUI5Ii8+IDwvcmRmOkRlc2NyaXB0aW9uPiA8L3JkZjpSREY+IDwveDp4bXBtZXRhPiA8P3hwYWNrZXQgZW5kPSJyIj8+TvKUhQAAExVJREFUeNpiFBVRY0AD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">
                  </div>

                  <div class="userinfo">
                    <div class="account">
                      <span class="accountName">李金胜</span>
                      &emsp;
                      <span class="accountNumber">账户：2023352</span>
                    </div>
                    <div class="confirm">
                      <span>
                        <Icon type="ios-checkmark-outline" size="20"></Icon>
                        身份证
                      </span>
                      <span>
                        <Icon type="ios-checkmark-outline" size="20"></Icon>
                        銀行卡
                      </span>
                      <span>
                        <Icon type="ios-checkmark" size="20"></Icon>
                        手機
                      </span>
                      <span>
                        <Icon type="ios-checkmark" size="20"></Icon>
                        郵箱
                      </span>
                    </div>
                  </div>
                </div>

              </div>
              <div class="headerRight">
                <div>
                  <div class="icons">
                    <Icon type="android-settings" size="30"></Icon>
                    <Icon type="power" size="30"></Icon>
                    <Badge count="1"><Icon type="ios-bell-outline" size="30"></Icon></Badge>
                    <Icon type="headphone" size="30"></Icon>
                  </div>
                  <div class="money">
                    <span class="balance">餘額:
                      <span class="balanceNumber"> $0.00 </span>
                    </span>
                    <span class="moneyIn">入金</span>
                    <span class="moneyOut">出金</span>
                  </div>
                </div>

              </div>
            </div>
          </Header>
          <Content :style="{margin: '20px', background: '#fff', minHeight: '260px'}">
            Content
            <router-view/>
          </Content>
        </Layout>
      </Layout>
    </div>

  </div>
</template>

<script>
export default {
  methods:{
    naviSelect(name){
      console.log(name);
      return name;
    }
  }
}
</script>

<style lang="scss">
// @import '~bootstrap/scss/bootstrap';
.ivu-menu-item {
  text-align: center;
}

.layout {
  border: 1px solid #d7dde4;
  background: #f5f7f9;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
}
.layout-header-bar {
  background: #fff;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
  height: 200px;
}

.header {
  background: url(http://p1z199nte.bkt.clouddn.com/static/img/user_top_pic.a7b9bd3.jpg)
    no-repeat top;
  display: flex;
  justify-content: space-between;
  height: 100%;

  .headerLeft {
    width: 30%;
    display: flex;
    align-items: center;

    & > div {
      display: flex;
      flex-direction: row;
      width: 90%;
      margin-left: 5%;

      .avatar {
        display: flex;
        align-items: center;
      }
      .userinfo {
        width: 80%;
        line-height: 36px;

        .account {
          margin-left: 6%;
          .accountName {
            font-size: 24px;
          }
          .accountNumber {
            font-size: 16px;
          }
        }
        .confirm {
          display: flex;
          justify-content: space-around;

          & span {
            cursor: pointer;
          }
        }
      }
    }
  }

  .headerRight {
    border: #5b6270 1px solid;
    width: 30%;
    display: flex;
    justify-content: flex-end;
    align-items: center;

    & > div {
      height: 80%;
      display: flex;
      flex-direction: column;
      //   display: flex;
      //   flex-direction: column;
      //   justify-content: flex-end;

      .icons {
        width: 200px;
        margin-right: 10px;
        display: flex;
        justify-content: space-around;
      }

      .money {
        margin-top: 20px;

        .balance {
          font-size: 14px;
        }
        .balanceNumber {
          font-size: 28px;
        }
      }
    }
  }
}

.layout-logo-left {
  width: 90%;
  height: 30px;
  background: #5b6270;
  border-radius: 3px;
  margin: 15px auto;
}
.menu-icon {
  transition: all 0.3s;
}
.rotate-icon {
  transform: rotate(-90deg);
}
.menu-item span {
  display: inline-block;
  overflow: hidden;
  width: 69px;
  text-overflow: ellipsis;
  white-space: nowrap;
  vertical-align: bottom;
  transition: width 0.2s ease 0.2s;
}
.menu-item i {
  transform: translateX(0px);
  transition: font-size 0.2s ease, transform 0.2s ease;
  vertical-align: middle;
  font-size: 16px;
}
.collapsed-menu span {
  width: 0px;
  transition: width 0.2s ease;
}
.collapsed-menu i {
  transform: translateX(5px);
  transition: font-size 0.2s ease 0.2s, transform 0.2s ease 0.2s;
  vertical-align: middle;
  font-size: 22px;
}
</style>
