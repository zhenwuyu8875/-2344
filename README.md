# Getting Started with Create React App

## 技术栈
React + ethers.js + IPFS + supabase + metamask

## 代码上传到Github
1. 创建Github账号
2. Windows安装git
3. 创建仓库
4. git clone 仓库地址
5. git add .
6. git commit -m "提交信息"
7. git push origin master


## 项目安装
1. 安装nodejs，https://nodejs.org/en/
至少v16
2. 进入到源码目录，安装依赖包
```bash
npm install
```
3. 本地运行
```bash
npm run start
```
在本地浏览器打开 http://localhost:3000
4. 打包
```bash
npm run build
```

## 代码结构

```bash
package.json # 项目配置文件
public/ # 静态资源
src/ # 源码目录
  assets/ # 静态资源
  components/ # 组件
    - Navbar.jsx # 导航栏
  pages/ # 页面
    - student/index.js # 学生页面
    - teacher/index.js # 老师页面
  utils/ # 工具类
    - OpenSeaTestABI.json # NFT合约ABI
  Contest  
    - Contest.jsx # 后端API ,和合约进行交互判断后存储信息
  App.js # 入口文件
  index.js # 入口文件
  Home.jsx # 首页

```


## 合约交互

### 合约
solidity合约代码
https://remix.ethereum.org/ # 在线编译合约，包括部署

- 入门学习文档
https://wtf.academy/

### ethers.js文档
https://docs.ethers.org/v5/

####  使用的API
```bash
const openseaTestContract = new ethers.Contract(OpenseaTestContractAddress, OpenSeaTestABI, provider);
const teacherTokenIds = '89099581206133984420867835859143877944362923373453247343276904189057008926820'; // 要查询余额的ERC1155代币的ID
const teacherBalances = await openseaTestContract.balanceOf(currentAccount, teacherTokenIds.toString());
console.log("hold teacher nft account: ",teacherBalances.toString()); // 输出代币余额
```
### ChainID
https://chainlist.org/chain/5


### 部署
使用：
https://www.netlify.com/

和Github关联，部署到网上
涉及授权代码仓库，需要在Github上设置




## 方案思路
学生和老师需要通过metamask钱包登录系统，并使用NFT管理学生和老师身份，使用IPFS去中心化存储管理系统的NFT，系统管理员会给 学生和老师的钱包地址分别空投学生NFT和老师NFT，  学生和老师通过metamask钱包登录系统后，持有学生NFT会进入到查询成绩页面，持有老师NFT的会进入到后台页面，可以录入、删除、修改学生成绩

## 细节拆分
1. 设计前端页面，包括登录页面、查询成绩页面、后台管理页面
2. 集成metamask钱包登录功能
3. 集成ether.js与以太坊交互，实现NFT的创建、转移、查询等功能
4. 集成IPFS去中心化存储，将NFT存储到IPFS上
5. 设计后端API，实现学生成绩的录入、删除、修改等功能
6. 集成后端API，与前端页面交互，实现学生成绩的管理功能

## 前端admin设计
1. 成绩列表页面，只支持查看学生对应成绩
2. 学生列表页面，支持增、删、改、查学生各种信息


## 与钱包交互
1. 钱包需要切换为goerli测试网络
2. MetaMask钱包签名后，会调用接口访问用户的NFT
这里需要做下判断，过滤下用户有没有持有NFT
    - 未持有NFT去联系管理员微信获取（线下联系方便管理员获取该用户的钱包地址等，不在页面做功能）
    - 持有学生NFT，显示查询成绩菜单，就是一个成绩列表
    - 持有老师NFT，显示增加、删除、修改成绩菜单
3. 管理员钱包必须有goerli测试网络ETH代币，可以从水龙头获取，用于支付发放NFT的gas费
网页挂机挖矿获得：https://goerli-faucet.pk910.de/

## NFT合约
通过opensea测试网上传图片生成NFT，https://testnets.opensea.io/
同样持有者转移需要gas费，这种更方便


## 后端逻辑设计
1. 学生表模型
2. 获得NFT后决定菜单权限

## 数据库
可以使用https://app.supabase.com/
使用Huawei@987123





## 注意事项
MetaMask存储在useState的数据属于前端的状态，可以通过清除浏览器缓存来删除。下面是清除MetaMask缓存的步骤：

在 MetaMask 扩展程序中，导航到菜单（位于左上角的三条横线）下的“设置”选项。
在设置页面的底部，点击“高级”选项卡。
点击“重置账户”按钮。
确认重置，等待MetaMask重新同步区块链状态。
这将会删除MetaMask扩展程序的所有数据，包括useState的状态。请注意，这将删除 MetaMask 中存储的所有账户和交易记录。如果您需要备份这些信息，请务必在重置之前导出您的账户私钥。