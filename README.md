### 项目来源

本项目来自 [vitozyf/lucky-draw: 年会抽奖程序](https://github.com/vitozyf/lucky-draw)

项目作者目前看起来似乎不再维护。由于百度分公司市场部活动采用，本人暂时维护。

# 年会抽奖

预览地址：[luckydraw](https://luckylottery.netlify.app/#/)

## 使用说明

### 配置建议

- 本程序理论支持配置百万级别人数，超过 10 万以上时初始化会比较耗时，初始化后可以正常抽奖。
- 如果人数较多，不建议导入名单或照片，按号码抽奖即可。

### 抽奖配置

- 设置抽奖总人数、奖项及每个奖项的人数，默认包含两个奖项，如果不想抽取默认的奖项，可以设置该奖项数量为 0
- 可以新增自定义的奖项，新增后必须将奖项人数设置大于 0 才会在抽奖奖项列表中显示

### 抽奖结果

- 显示抽取的结果，点击号码允许从结果中删除该号码。删除后该号码可以参与剩余的抽奖，否则已经中的号码无法参与剩余奖项的抽奖（除非开启全员参与功能）

### 开始

- 开始抽奖，需要选取抽取的奖项、本次抽取的人数和是否开启全员抽奖功能。
- 本次抽取的人数可以选择 1 人、5 人、一次性抽取完或者自定义抽取数量，不能大于奖项剩余的数量
- 点击停止抽取完成

### 重置

- 重置数据恢复到初始状态
- 可选的重置选项：
  `1.重置全部数据 2.重置抽奖配置 3.重置名单 4.重置照片 5.重置抽奖结果`

### 导入名单

- 按照格式导入名单，可以多次输入。若号码有对应的姓名，则在抽取过程及结果中会显示号码及姓名，若没有对应的姓名，则只显示号码。

### 导入相册

- 按照 抽奖号-照片的一对一导入，（可在现场将号码发出签到后，每发一个号码，导入一个照片）。抽奖结果将以照片形式展示。
- 照片格式支持`.jpg`和`.png`，照片大小不能超过 `150kb`,建议 `20-50kb`，建议尺寸为 `160*160px`

---
## 维护者添加

**经实际测试，原项目有两个问题:**

1. 生产环境下直接部署会产生资源404，这是由于 `vue.config.js` 中配置了生产模式下的路径，现已经解决。改为默认当前目录。

2. 当导入数据量过多(800以上)时，抽奖圆球的密度会过大，美观度不足。所以隐藏了部分显示，但实际抽奖还是从全部数据中抽的。

  修改过程：`src/app.vue` 文件：

  ```diff
      datas() {
        const { number } = this.config;
  -      const nums = number >= 1500 ? 500 : this.config.number;
  -      const configNum = number > 1500 ? Math.floor(number / 3) : number;
  +      const nums = number >= 800 ? 80 : this.config.number;
  +      const configNum = number;
        const randomShowNums = luckydrawHandler(configNum, [], nums);
      }
  ```
  将最大实际显示值从500改为80。

（其实上面这个问题可以在 `src/store/index.js` 中配置）

另外修改了下抽奖结果卡片的样式，这里不赘述。

**除以上问题外，这个库将原项目中的音效等去除，仅在代码中注释，资源文件和实际控件还保留。**

---
## 温馨提示

- 本抽奖程序无暗箱操作，无后台，无后门。
- 名单和照片显示只需导入一种即可,无导入数据则使用抽奖号码。
- 建议使用最新的 Chrome 浏览器打开体验最佳。
- <del>由于背景音乐加载较慢，可以在抽奖前提前打开缓存好。或者安装 windows 版本软件到本地，无需联网即可使用。</del>

## windows 软件版本

- 本抽奖程序的 windows 软件版本下载[安装包](https://github.com/vitozyf/lucky-draw/releases)

## License

[MIT](https://choosealicense.com/licenses/mit/)