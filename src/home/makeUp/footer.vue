<template>
  <div class="footer">
    <div class="area">
      <div class="links display align">
        <span class="link-text">相关链接</span>
        <div style="margin-left:53px">
          <el-select v-model="value1" placeholder="国家级网站" @change="jump" style="width:100%">
            <el-option
              v-for="(item,index) in options1"
              :key="index"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </div>
        <div style="margin:0 35px">
          <el-select v-model="value2" placeholder="广东省级网站" @change="jump" style="width:100%">
            <el-option
              v-for="(item,index) in options2"
              :key="index"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </div>
        <div>
          <el-select v-model="value3" placeholder="揭阳市相关网站" @change="jump" style="width:100%">
            <el-option
              v-for="(item,index) in options3"
              :key="index"
              :label="item.label"
              :value="item.value"
            ></el-option>
          </el-select>
        </div>
      </div>
      <div class="description">
        <div>
          <div class="description-contain">
            <div class="description-one">
              <span @click="push('/aboutMe')">关于我们</span>
              <span class="shu"></span>
              <span @click="push('/cityMap')">联系我们</span>
              <span class="shu"></span>
              <span @click="push('/aboutNav')">网址导航</span>
            </div>
            <div class="description-two">
              <span>
                <a
                  href="http://bszs.conac.cn/sitename?method=show&id=5316C12526B57C60E053012819ACB84D"
                  target="_blank"
                >
                  <img src="@/assets/image/home/causedw.png" alt />
                </a>
              </span>
              <span style="margin-right:20px">主办单位：揭阳市公共资源交易中心</span>
              <span>技术支持：深圳市壹平台信息技术有限公司</span>
              <span>
                <a href="http://121.43.68.40/exposure/jiucuo.html" target="_blank">
                  <img src="@/assets/image/home/findError.png" alt />
                </a>
              </span>
            </div>
          </div>
        </div>
        <div class="description-three display align">
          <span>网站标识码4452000082</span>

          <span class="display align">
            <img src="@/assets/image/home/gongan.png" alt style="margin-right:8px" />
            粤公网安备44520202000313号
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      options1: [
        // {
        //   value: "http://www.mohurd.gov.cn/",
        //   label: "中华人民共和国住房和城乡建设部",
        // },
        // {
        //   value: "http://www.mof.gov.cn/index.htm",
        //   label: "中华人民共和国财政部",
        // },
        // {
        //   value: "https://www.ndrc.gov.cn/",
        //   label: "中华人民共和国国家发展和改革委员会",
        // },
      ],
      options2: [
        // {
        //   value: "http://zfcxjst.gd.gov.cn/",
        //   label: "广东省住房和城乡建设厅",
        // },
        // {
        //   value: "http://czt.gd.gov.cn/",
        //   label: "广东省财政厅",
        // },
        // {
        //   value: "http://drc.gd.gov.cn/",
        //   label: "广东省发展和改革委员会",
        // },
      ],
      options3: [
        // {
        //   value: "http://www.jieyang.gov.cn/zjj/",
        //   label: "揭阳市住房和城乡建设局官方网站",
        // },
        // {
        //   value: "http://www.jieyang.gov.cn/jycz/",
        //   label: "揭阳市财政局",
        // },
        // {
        //   value: "https://www.baidu.com/",
        //   label: "揭阳市发展和改革委员局",
        // },
      ],
      value1: "",
      value2: "",
      value3: "",
    };
  },
  created() {
    this.queryCms("010001");
    this.queryCms("010002");
    this.queryCms("010003");
  },
  methods: {
    push(path) {
      let name = "";
      switch (path) {
        case "/aboutMe":
          name = "关于我们";
          break;
        case "/callMe":
          name = "联系我们";
          break;
        case "/aboutNav":
          name = "网址导航";
          break;
      }
      let params = {
        path: path,
        name: name,
      };
      this.$store.commit("add_tabs", params);
      this.$router.push(path);
    },
    jump(value) {
      window.open(value);
    },
    toError() {
      window.open("http://121.43.68.40/exposure/jiucuo.html");
    },
    queryCms(val) {
      // let res = await this.$axios.get(
      //   "/api/ords/epfcms/cmsItem/queryCmsItemBySeriesId/" + val
      // );
      this.$axios
        .get("/api/ords/epfcms/cmsItem/queryCmsItemBySeriesId/" + val)
        .then((res) => {
          let data = res.data.items;
          if (data) {
            data.forEach((elem) => {
              let obj = {};
              if (val == "010001") {
                obj.label = elem.name;
                obj.value = elem.url;
                this.options1.push(obj);
              } else if (val == "010002") {
                obj.label = elem.name;
                obj.value = elem.url;
                this.options2.push(obj);
              } else if (val == "010003") {
                obj.label = elem.name;
                obj.value = elem.url;
                this.options3.push(obj);
              }
            });
          }
        });
    },
  },
};
</script>

<style  scoped>
.footer {
  height: 196px;
  background: #3854b8;
}
.links {
  height: 60px;
  padding: 0 10px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.11);
}
.links > div {
  width: 330px;
}
.link-text {
  font-weight: bold;
  font-size: 16px;
  color: rgba(255, 255, 255, 1);
}
.description {
  font-size: 16px;
  margin-top: 20px;
}
.description > div {
  display: flex;
  justify-content: center;
  color: #fff;
}
.description-one {
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
}
.description-one span {
  cursor: pointer;
}
.description-two img {
  vertical-align: middle;
  margin: 0 20px;
}

.description-three {
  font-size: 14px;
  /* margin-top: 20px; */
}
.description-three span {
  margin: 0 20px;
}

.description-contain {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.shu {
  height: 12px;
  width: 1px;
  background: #fff;

  margin: 0 10px;
}
</style>
<style>
.footer .el-input__inner {
  height: 32px;
  line-height: 32px;
  border-radius: 17px;
  color: #3854b8;
  font-size: 16px;
}
.footer .el-input__icon {
  line-height: 32px;
}
.footer .el-icon-arrow-up:before {
  content: "";
}
.footer .el-input__icon {
  background: url("../../assets/image/home/select2.png") no-repeat 5px 8px;
}
.footer input::-webkit-input-placeholder {
  color: #3854b8;
}
.footer input::-moz-placeholder {
  /* Mozilla Firefox 19+ */
  color: #3854b8;
}
.footer input:-moz-placeholder {
  /* Mozilla Firefox 4 to 18 */
  color: #3854b8;
}
.footer input:-ms-input-placeholder {
  /* Internet Explorer 10-11 */
  color: #3854b8;
}
</style>