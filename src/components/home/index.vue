<template>
  <div>
    <el-row>
      <h3>
        Cards
        <i class="annotation">View all cards</i>
      </h3>
      <el-col
        :xs="24"
        :sm="24"
        :md="8"
        :lg="8"
        :xl="8"
        v-for="(item,index) in fakeData"
        :key="index"
        style="margin-bottom:15px;"
      >
        <div :class="['card-box', item.bankColor]">
          <p class="margin0">{{item.bankName}}</p>
          <h4 class="margin0 margin-b20 color-white">{{item.balance}}</h4>
          <p class="margin0">{{item.number}}</p>
          <div class="footer-name">
            <h3 class="margin0 color-white">{{item.userName}}</h3>
            <el-switch
              class="pull-right"
              v-model="item.state"
              active-color="#13ce66"
              inactive-color="#ff4949"
            ></el-switch>
          </div>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8">
        <el-upload
          class="avatar-uploader card-box-uploader"
          action="https://jsonplaceholder.typicode.com/posts/"
          :show-file-list="false"
          :on-success="handleAvatarSuccess"
          :before-upload="beforeAvatarUpload"
        >
          <img v-if="imageUrl" :src="imageUrl" class="avatar" />
          <i v-else class="el-icon-plus avatar-uploader-icon"></i>
        </el-upload>
      </el-col>
    </el-row>
    <el-row>
      <el-col :xs="24" :sm="24" :md="8" :lg="6" :xl="4">
        <h3>
          Main Services
          <i class="annotation">View all</i>
        </h3>
        <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
          <div class="services-box">
            <i class="el-icon-delete"></i>
            <p>Transactions</p>
          </div>
        </el-col>
        <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12">
          <div class="services-box">
            <i class="el-icon-delete"></i>
            <p>Transactions</p>
          </div>
        </el-col>
      </el-col>
      <el-col :xs="24" :sm="24" :md="14" :lg="16" :xl="18" style="padding-left: 20px;">
        <h3>
          Current
          <i class="annotation">View all</i>
        </h3>
        <el-row>
          <h3>
            Savings
            <i class="annotation">View all</i>
          </h3>
          <el-col :xs="24" :sm="24" :md="24" :lg="24" :xl="24">
            <div id="charts1" :style="{width: '100%', height: '300px'}"></div>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import "echarts/lib/chart/line";
import "echarts/lib/chart/pie";
export default {
  data() {
    return {
      value: true,
      imageUrl: "",
      fakeData: [
        //假数据循环出来
        {
          bankName: "Availlable balance",
          balance: "$ 2,200",
          number: "**********34",
          userName: "Monzo",
          state: true,
          bankColor: "red"
        },
        {
          bankName: "Availlable balance",
          balance: "$ 2,200",
          number: "**********34",
          userName: "Monzo",
          state: true,
          bankColor: "green"
        }
      ],
      numberList: [
        {
          num1: "1063873637834",
          num2: "$2,200.01"
        },
        {
          num1: "1063873637834",
          num2: "$2,200.01"
        },
        {
          num1: "1063873637834",
          num2: "$2,200.01"
        }
      ],
      myChart: null
    };
  },
  mounted() {
    this.drawLine();
    // let myChart = this.$echarts.init(document.getElementById("charts1"));
    window.onresize = () => {
      if (this.myChart) {
        this.myChart.resize();
      }
      //在屏幕大小发生改变时 改变大小

      // this.drawLine();
    };
  },
  methods: {
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      this.myChart = this.$echarts.init(document.getElementById("charts1"));
      // 绘制图表
      this.myChart.setOption({
        title: { text: "线形图" },
        tooltip: {},
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            data: [820, 932, 901, 934, 1290, 1330, 1320],
            type: "line",
            smooth: false
          }
        ]
      });
    },
    handleAvatarSuccess(res, file) {
      this.imageUrl = URL.createObjectURL(file.raw);
    },
    beforeAvatarUpload(file) {
      //限制图片类型和大小
      const isJPG = file.type === "image/jpeg";
      const isLt2M = file.size / 1024 / 1024 < 2;

      if (!isJPG) {
        this.$message.error("上传头像图片只能是 JPG 格式!");
      }
      if (!isLt2M) {
        this.$message.error("上传头像图片大小不能超过 2MB!");
      }
      return isJPG && isLt2M;
    }
  }
};
</script>

<style>
.avatar-uploader .el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  width: 100%;
  height: 130px;
}
.avatar-uploader .el-upload:hover {
  border-color: #409eff;
}
.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  line-height: 130px;
  text-align: center;
  width: 100%;
  height: 130px;
}
.avatar-uploader .el-icon-plus:before {
  line-height: 130px;
}
.avatar {
  width: 100%;
  height: 130px;
  display: block;
}
.annotation {
  color: #909399;
  font-size: 12px;
  float: right;
  line-height: 24px;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.margin0 {
  margin: 0;
}
.card-box {
  margin: 0 5px;
  padding: 20px;
  padding-bottom: 35px;
  border-radius: 10px;
}
.card-box-uploader {
  margin: 0 5px;
  border-radius: 10px;
}
.card-box.red {
  background: rgba(238, 54, 54, 0.81);
  color: #ee3636;
}
.card-box.green {
  background: #381990d1;
}
.footer-name .el-switch {
  position: absolute;
  right: 0;
}
.footer-name {
  position: relative;
}
.footer-name > h3 {
  position: absolute;
}
.color-white {
  color: white;
}
.margin-b20 {
  margin-bottom: 20px;
}
.services-box {
  border-radius: 25px;
  padding: 8px;
  text-align: center;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
.services-box > i {
  margin-top: 5px;
  font-size: 40px;
  color: #e36d2f;
}
</style>