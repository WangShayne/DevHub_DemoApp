<template>
  <el-card class="box-card">
    <div slot="header" class="clearfix">
      <span class="card-title">Interior Lightning Service</span>
      <el-button
        style="float: right; padding: 3px 0; color: #ec7211"
        type="text"
        >Service description<i
          class="el-icon-arrow-right el-icon--right"
          style="vertical-align: text-bottom"
        ></i
      ></el-button>
      <el-divider></el-divider>
    </div>
    <div class="card-body">
      <div class="left">
        <template v-for="(item, index) in information">
          <div class="desc" :key="index">
            <span class="desc-title">{{ item.name }}:</span>
            <span class="desc-content">{{ item.value }}</span>
          </div>
        </template>
      </div>
      <div class="right">
        <h3 style="color: #ec7211">Full Refund</h3>
        <template v-for="(item, index) in paid">
          <div class="refund" :key="index">
            <span class="refund-title"
              >{{ item.name }} <i class="el-icon-question"></i
            ></span>
            <span class="refund-content">${{ item.value }}</span>
          </div>
        </template>
      </div>
    </div>
    <el-divider class="footer-divider"></el-divider>
    <div class="card-footer">
      <h4 class="canceled">Booking Canceled</h4>
    </div>
  </el-card>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "Service description",
    },
    information: {
      type: Array,
      default: () => [],
    },
    paid: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style lang="scss" scoped>
.box-card {
  width: 800px;

  ::v-deep .el-card__header {
    padding-bottom: 0;
    border: none;
  }
  ::v-deep .el-divider--horizontal {
    margin-top: 20px;
    margin-bottom: 10px;
  }
  .card-title {
    font-size: 22px;
    font-weight: 500;
  }
  .card-body {
    display: flex;
    .left {
      display: flex;
      flex-wrap: wrap;
      width: 500px;
      .desc {
        display: flex;
        flex-direction: column;
        min-width: 200px;
        margin-bottom: 20px;
        color: #666;
        .desc-title {
          margin-bottom: 6px;
        }
        .desc-content {
          font-size: 20px;
          font-weight: 500;
        }
      }
    }
    .right {
      position: relative;
      padding-left: 40px;
      &::before {
        position: absolute;
        top: 50%;
        left: 0;
        display: block;
        content: "";
        width: 1px;
        height: 100%;
        background: #aaa;
        transform: translateX(-50%) translateY(-50%);
      }
      .refund {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
        font-size: 24px;
        font-weight: 500;
        color: #555;
        .refund-title {
          i {
            font-size: 18px;
          }
        }
      }
    }
  }
  .footer-divider {
    height: 4px;
  }
  .card-footer {
    margin-bottom: 10px;
    .canceled {
      text-align: right;
      color: #333;
    }
  }
}
</style>