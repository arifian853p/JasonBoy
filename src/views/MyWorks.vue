<template>
  <div class="works-container">
    <el-page-header @back="goBack" content="我的作品"> </el-page-header>
    <div style="display: flex">
      <div>
        <div class="heji">
          <div>当前合集数:{{ collection.length }}</div>
          <el-button class="btn" @click="dialogVisible = true"
            >创建新合集</el-button
          >
        </div>
        <el-dialog title="创建合集" :visible.sync="dialogVisible" width="30%">
          <el-form ref="form" :model="form" label-width="120px">
            <el-form-item label="请输入合集名称">
              <el-input v-model="form.name"></el-input>
            </el-form-item>
          </el-form>
          <span slot="footer" class="dialog-footer">
            <el-button @click="dialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="confirm">确 定</el-button>
          </span>
        </el-dialog>
        <div class="works">
          <el-collapse v-model="activeNames">
            <el-collapse-item v-for="(i, n) in collection" :key="n">
              <template class="work-title" slot="title">
                {{ i.title }}
              </template>
              <div class="work" v-for="(a, b) in i.content" :key="b">
                <img :src="a.imgUrl" alt="" />
                <div class="info">
                  <div class="name">{{ a.name }}</div>
                  <div class="classify">分类：{{ a.classify }}</div>
                  <div class="brief">简介：{{ a.brief }}</div>
                </div>
              </div>
            </el-collapse-item>
          </el-collapse>
        </div>
      </div>
      <div class="nocollection">
        <div>未加入合集</div>
        <div class="noworks">
          <div class="nowork" v-for="(i,n) in nocollection" :key="n">
            <img :src="i.imgUrl" alt="" />
            <div class="info">
              <div class="name">名称：{{i.name}}</div>
              <div class="classify">分类：{{i.classify}}</div>
              <div class="brief">简介：{{i.brief}}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeNames: ["1"],
      dialogVisible: false,
      form: { name: "" },
      collection: [
        {
          title: "纳新的合集一",
          content: [
            {
              imgUrl:
                "https://img0.baidu.com/it/u=3068939878,3205715933&fm=253&fmt=auto&app=138&f=JPG?w=624&h=467",
              name: "小蝌蚪找妈妈",
              classify: "儿童",
              brief: "这是一篇有爱的读物",
            },
            {
              imgUrl:
                "https://img1.baidu.com/it/u=2679251038,2627501571&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=677",
              name: "女娲补天",
              classify: "神话故事",
              brief: "女娲补天的故事",
            },
            {
              imgUrl:
                "https://img1.baidu.com/it/u=4288287645,2912178016&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=592",
              name: "嫦娥奔月",
              classify: "神话故事",
              brief: "嫦娥奔月神话故事",
            },
            {
              imgUrl:
                "https://img2.baidu.com/it/u=1788868896,90411196&fm=253&fmt=auto&app=138&f=JPEG?w=700&h=400",
              name: "猴子捞月",
              classify: "寓言故事",
              brief: "猴子捞月的故事",
            },
          ],
        },
        {
          title: "纳新的合集二",
        },
        {
          title: "纳新的合集三",
        },
        {
          title: "纳新的合集四",
        },
      ],
      nocollection: [
        {
          imgUrl:
            "https://img0.baidu.com/it/u=2017485733,2235813138&fm=253&fmt=auto&app=138&f=PNG?w=497&h=500",
          name: "乌鸦喝水",
          classify: "寓言故事",
        },
        {
          imgUrl:
            "https://img0.baidu.com/it/u=2017485733,2235813138&fm=253&fmt=auto&app=138&f=PNG?w=497&h=500",
          name: "乌鸦喝水",
          classify: "寓言故事",
        },
      ],

    };
  },
  methods: {
    goBack() {
      this.$router.back();
    },
    confirm() {
      this.dialogVisible = false;
      this.collection.push({ title: this.form.name });
      this.form.name = "";
    },
  },
};
</script>

<style lang="less" scoped>
.works-container {
  width: 1180px;
  padding: 50px 0;
  margin: 0 auto;
  background-color: #fff;
  .heji {
    margin-left: 90px;
    margin-top: 20px;
    display: flex;
    align-items: center;
    .btn {
      margin-left: 20px;
    }
  }

  .works {
    width: 500px;
    margin-left: 90px;
    margin-top: 20px;

    .image {
      width: 50px;
      height: 50px;
    }

    .work {
      display: flex;
      align-items: center;
      margin-top: 10px;
      img {
        width: 100px;
        height: 100px;
      }
      .info {
        margin-left: 20px;
      }
    }
  }
  .nocollection {
    margin-top: 20px;
    margin-left: 40px;
    .noworks {
        display: flex;
      .nowork {
        display: flex;
        align-items: center;
        margin-top: 20px;
        width: 260px;
        height: 100px;
        border: 1px solid #ccc;
        margin-right: 10px;
        img {
          width: 85x;
          height: 95px;
        }
        .info {
            margin-left: 20px;
        }
      }
    }
  }
}
</style>