![](blob:https://www.doubao.com/783b661c-97a1-4cfb-9d2f-d9006f104a58)

参照页面设计前端功能进行对接
  
### 复盘盒子 App 前端对接方案（参照页面设计）  
  
基于截图中的**复盘盒子 - 超短打板好帮手**页面设计，前端对接需覆盖**页面结构、核心模块、交互逻辑、数据接口**四大维度，以下是分模块对接方案：  
  
### 一、页面整体结构与布局  
  
#### 1. 顶部信息区（App Store 展示页头部）  
  
- **核心元素**：App 图标、标题（复盘盒子 - 超短打板好帮手）、副标题（Utility）、标签（免费 + 内购、iPad 适配）、分享按钮、筛选标签（18+、分类、开发者、语言、大小）  
- **前端对接要点**：  
- 布局：采用**Flex/Grid**实现响应式，适配 PC / 移动端展示；  
- 数据：静态展示（标题、图标）+ 接口获取（开发者、大小、语言等）；  
- 样式：渐变背景（紫蓝渐变）、圆角图标、文字层级（标题粗体，副标题浅灰）。  
  
#### 2. 核心功能轮播区（5 张功能卡片）  
  
- **核心元素**：题材轮动、连板梯队、题材概览、热门题材、个股详情 5 个功能模块，每个模块含**标题、副标题、手机 Mock 图、功能说明**  
- **前端对接要点**：  
- 轮播组件：使用`Swiper.js`实现横向滑动，支持手势 / 点击切换，添加分页指示器；  
- 卡片样式：深色背景（深蓝 / 黑）、渐变点缀、手机 Mock 图居中、文字左对齐（功能标题粗体，说明浅灰）；  
- 交互：hover 时卡片轻微上浮，切换时添加淡入淡出动画。  
  
### 二、核心功能模块前端对接（按卡片拆分）  
  
#### 1. 题材轮动模块  
  
- **页面元素**：题材列表（题材名称、涨幅、连板数）、筛选按钮（按涨幅 / 连板 / 热度）、数据卡片（题材核心数据）  
- **前端对接**：  
- 接口：`/api/theme/rotation`（获取题材轮动数据）、`/api/theme/filter`（筛选题材）；  
- 组件：表格组件（支持排序、分页）、筛选按钮组（单选 / 多选）、数据卡片（展示核心指标）；  
- 交互：点击题材行，跳转至**题材概览**详情页；筛选按钮点击后实时刷新表格数据。  
  
#### 2. 连板梯队模块  
  
- **页面元素**：连板股票列表（股票名称、代码、连板数、涨幅、封单额）、梯队分类（1 板 / 2 板 / 3 板 +）、涨停 / 跌停标识  
- **前端对接**：  
- 接口：`/api/stock/limit-up`（获取连板梯队数据）；  
- 组件：分类标签页（切换不同连板数梯队）、股票列表（支持按连板数 / 涨幅排序）、状态标签（涨停红、跌停绿）；  
- 交互：点击股票行，跳转至**个股详情**页；梯队标签切换时，列表数据实时更新。  
  
#### 3. 题材概览模块  
  
- **页面元素**：题材基础信息（名称、热度、涨幅）、成分股列表（股票名称、涨幅、市值）、题材趋势图（K 线 / 折线图）  
- **前端对接**：  
- 接口：`/api/theme/detail/{themeId}`（获取题材详情）、`/api/theme/trend/{themeId}`（获取题材趋势数据）；  
- 组件：信息卡片（展示题材基础数据）、成分股表格、ECharts/Chart.js 绘制趋势图；  
- 交互：点击成分股，跳转至**个股详情**；趋势图支持缩放、 tooltip 悬浮展示数据。  
  
#### 4. 热门题材模块  
  
- **页面元素**：热门题材排行榜（题材名称、热度值、涨幅、相关个股数）、题材分类（光伏 / 电子 / 锂电池等）、热度趋势标识  
- **前端对接**：  
- 接口：`/api/theme/hot`（获取热门题材数据）；  
- 组件：排行榜列表（支持按热度 / 涨幅排序）、分类筛选（下拉 / 标签筛选）、热度趋势图标（上升 / 下降箭头）；  
- 交互：点击题材，跳转至**题材概览**页；筛选后实时刷新排行榜。  
  
#### 5. 个股详情模块  
  
- **页面元素**：个股基础信息（名称、代码、现价、涨跌幅、成交量）、财务数据（营收、净利润、市盈率）、K 线图、分时图、相关题材  
- **前端对接**：  
- 接口：`/api/stock/detail/{stockCode}`（获取个股详情）、`/api/stock/kline/{stockCode}`（获取 K 线数据）、`/api/stock/finance/{stockCode}`（获取财务数据）；  
- 组件：信息卡片（基础数据）、ECharts 绘制 K 线 / 分时图、财务数据表格、相关题材标签；  
- 交互：K 线图支持切换周期（日 / 周 / 月）、tooltip 悬浮展示；相关题材点击跳转至**题材概览**。  
  
### 三、前端技术栈与对接规范  
  
#### 1. 技术栈选型  
  
- **框架**：Vue3（Composition API）/ React18（Hooks），适配移动端 / PC 端；  
- **UI 组件**：Vant（移动端）/ Element Plus（PC 端），自定义深色主题（匹配设计稿深蓝 / 黑风格）；  
- **图表库**：ECharts（K 线 / 趋势图）、Chart.js（简易图表）；  
- **轮播 / 交互**：Swiper.js（轮播）、GSAP（动画）；  
- **网络请求**：Axios（封装请求拦截、响应拦截，统一处理接口异常）；  
- **样式**：Less/Sass（变量管理主题色、圆角、间距），Tailwind CSS（快速布局）。  
  
#### 2. 接口对接规范  
  
- **请求方式**：GET（数据查询）、POST（筛选 / 提交）；  
- **参数规范**：  
- 分页：`pageNum`、`pageSize`；  
- 筛选：`themeType`、`limitUpNum`、`sortType`（排序方式）；  
- 详情：`themeId`、`stockCode`（路径参数）；  
- **响应规范**：  
  
json  
  
```json  
{  
"code": 200, // 200成功，500失败，401未授权  
"msg": "success",  
"data": {  
// 业务数据  
"list": [],  
"total": 100,  
"detail": {}  
}  
}  
```  
  
- **异常处理**：接口报错时，弹出 Toast 提示；无数据时展示空状态组件。  
  
#### 3. 样式与交互规范  
  
- **主题色**：主色 #2A2D56（深蓝）、辅助色 #6C63FF（紫）、强调色 #FF4757（红，涨停）、#00D2D3（绿，跌停）；  
- **字体**：标题用`PingFang SC Bold`，正文用`PingFang SC Regular`，数字用等宽字体；  
- **交互**：  
- 点击反馈：按钮 / 卡片点击时添加阴影 / 缩放效果；  
- 加载状态：数据请求时展示骨架屏 / Loading 动画；  
- 响应式：移动端竖屏 / 横屏适配，PC 端适配不同分辨率。  
  
### 四、对接流程与注意事项  
  
1. **静态页面还原**：先按设计稿实现 5 个功能模块的静态页面，还原样式、布局、交互；  
2. **接口联调**：按模块对接后端接口，先 mock 数据调试，再联调真实接口；  
3. **功能测试**：测试数据渲染、筛选、排序、跳转、图表展示等核心功能；  
4. **兼容性适配**：测试 iOS/Android、Chrome/Safari 等不同设备与浏览器的兼容性；  
5. **性能优化**：图片懒加载、接口防抖 / 节流、虚拟列表（长列表数据）、图表按需渲染。  
  
### 五、交付物  
  
1. 前端代码（Vue/React 工程化项目，含组件、接口、样式）；  
2. 接口对接文档（接口地址、参数、响应、异常处理）；  
3. 页面适配报告（不同设备 / 浏览器的适配效果）；  
4. 功能测试报告（核心功能测试用例与结果）。  
  
你希望我提供 Vue/React 组件代码模板（题材轮动表格、连板梯队标签页）以及 Axios 封装示例，我会分别给出基于 Vue3 + Element Plus 和 React18 + Ant Design 的完整可运行代码模板，同时包含通用的 Axios 封装方案。  
  
---  
  
## 一、通用 Axios 封装示例（前后端通用）  
这是项目中最基础也最核心的请求封装，包含请求/响应拦截、统一错误处理、请求取消等最佳实践。  
  
```javascript  
// src/utils/request.js  
import axios from 'axios';  
import { ElMessage, ElLoading } from 'element-plus'; // Vue3 按需引入  
// React 请替换为 antd 的 message/Spin：import { message, Spin } from 'antd';  
  
// 创建axios实例  
const service = axios.create({  
baseURL: import.meta.env.VITE_API_BASE_URL || '/api', // 环境变量配置  
timeout: 10000, // 请求超时时间  
headers: {  
'Content-Type': 'application/json;charset=UTF-8'  
}  
});  
  
// 加载中实例  
let loadingInstance = null;  
  
// 请求拦截器  
service.interceptors.request.use(  
(config) => {  
// 显示加载中（可根据config配置是否显示）  
if (config.showLoading !== false) {  
loadingInstance = ElLoading.service({  
lock: true,  
text: '数据加载中...',  
background: 'rgba(0, 0, 0, 0.7)'  
});  
}  
  
// 添加token（登录态）  
const token = localStorage.getItem('token');  
if (token) {  
config.headers.Authorization = `Bearer ${token}`;  
}  
  
return config;  
},  
(error) => {  
// 关闭加载中  
if (loadingInstance) loadingInstance.close();  
ElMessage.error('请求发送失败，请稍后重试');  
return Promise.reject(error);  
}  
);  
  
// 响应拦截器  
service.interceptors.response.use(  
(response) => {  
// 关闭加载中  
if (loadingInstance) loadingInstance.close();  
  
const res = response.data;  
// 业务状态码判断（根据后端约定调整）  
if (res.code !== 200) {  
ElMessage.error(res.msg || '请求失败');  
// 401未授权，跳转到登录页  
if (res.code === 401) {  
localStorage.removeItem('token');  
window.location.href = '/login';  
}  
return Promise.reject(res);  
}  
return res;  
},  
(error) => {  
// 关闭加载中  
if (loadingInstance) loadingInstance.close();  
  
// 网络错误处理  
let errMsg = '网络异常，请检查网络连接';  
if (error.response) {  
const status = error.response.status;  
switch (status) {  
case 404:  
errMsg = '请求地址不存在';  
break;  
case 500:  
errMsg = '服务器内部错误';  
break;  
default:  
errMsg = `请求错误 ${status}`;  
}  
}  
ElMessage.error(errMsg);  
return Promise.reject(error);  
}  
);  
  
// 封装请求方法  
const request = {  
get(url, params = {}, config = {}) {  
return service.get(url, { params, ...config });  
},  
post(url, data = {}, config = {}) {  
return service.post(url, data, config);  
},  
put(url, data = {}, config = {}) {  
return service.put(url, data, config);  
},  
delete(url, params = {}, config = {}) {  
return service.delete(url, { params, ...config });  
}  
};  
  
export default request;  
```  
  
## 二、Vue3 + Element Plus 组件模板  
### 1. 题材轮动表格组件（ThemeRotation.vue）  
```vue  
<template>  
<div class="theme-rotation-container">  
<!-- 筛选栏 -->  
<div class="filter-bar">  
<el-button-group>  
<el-button  
v-for="item in sortOptions"  
:key="item.value"  
:type="activeSort === item.value ? 'primary' : 'default'"  
@click="handleSortChange(item.value)"  
>  
{{ item.label }}  
</el-button>  
</el-button-group>  
</div>  
  
<!-- 题材轮动表格 -->  
<el-table  
:data="themeList"  
border  
stripe  
v-loading="loading"  
@row-click="handleRowClick"  
>  
<el-table-column  
prop="themeName"  
label="题材名称"  
min-width="150"  
/>  
<el-table-column  
prop="riseRate"  
label="涨幅(%)"  
width="100"  
>  
<template #default="scope">  
<span :class="scope.row.riseRate >= 0 ? 'text-red' : 'text-green'">  
{{ scope.row.riseRate.toFixed(2) }}  
</span>  
</template>  
</el-table-column>  
<el-table-column  
prop="boardNum"  
label="连板数"  
width="100"  
/>  
<el-table-column  
prop="hotValue"  
label="热度值"  
width="100"  
/>  
<el-table-column  
label="操作"  
width="100"  
>  
<template #default="scope">  
<el-button  
type="text"  
@click="viewDetail(scope.row)"  
>  
详情  
</el-button>  
</template>  
</el-table-column>  
</el-table>  
  
<!-- 分页 -->  
<el-pagination  
v-model:current-page="pageNum"  
v-model:page-size="pageSize"  
:total="total"  
layout="prev, pager, next, jumper, ->, total"  
@size-change="handlePageChange"  
@current-change="handlePageChange"  
class="pagination"  
/>  
</div>  
</template>  
  
<script setup>  
import { ref, onMounted } from 'vue';  
import request from '@/utils/request';  
import { useRouter } from 'vue-router';  
  
const router = useRouter();  
  
// 响应式数据  
const loading = ref(false);  
const themeList = ref([]);  
const total = ref(0);  
const pageNum = ref(1);  
const pageSize = ref(10);  
const activeSort = ref('riseRate'); // 默认按涨幅排序  
  
// 排序选项  
const sortOptions = [  
{ label: '按涨幅排序', value: 'riseRate' },  
{ label: '按连板数排序', value: 'boardNum' },  
{ label: '按热度排序', value: 'hotValue' }  
];  
  
// 获取题材轮动数据  
const getThemeRotationData = async () => {  
loading.value = true;  
try {  
const res = await request.get('/theme/rotation', {  
pageNum,  
pageSize,  
sortType: activeSort.value  
}, { showLoading: false }); // 手动控制loading，避免重复显示  
  
themeList.value = res.data.list;  
total.value = res.data.total;  
} catch (err) {  
console.error('获取题材轮动数据失败：', err);  
} finally {  
loading.value = false;  
}  
};  
  
// 排序切换  
const handleSortChange = (sortType) => {  
activeSort.value = sortType;  
pageNum.value = 1; // 排序切换重置页码  
getThemeRotationData();  
};  
  
// 分页变化  
const handlePageChange = () => {  
getThemeRotationData();  
};  
  
// 行点击事件  
const handleRowClick = (row) => {  
viewDetail(row);  
};  
  
// 查看题材详情  
const viewDetail = (row) => {  
router.push({  
path: '/theme/detail',  
query: { themeId: row.themeId }  
});  
};  
  
// 初始化加载数据  
onMounted(() => {  
getThemeRotationData();  
});  
</script>  
  
<style scoped>  
.theme-rotation-container {  
padding: 20px;  
background: #fff;  
border-radius: 8px;  
}  
  
.filter-bar {  
margin-bottom: 16px;  
}  
  
.text-red {  
color: #f56c6c;  
}  
  
.text-green {  
color: #67c23a;  
}  
  
.pagination {  
margin-top: 20px;  
text-align: right;  
}  
</style>  
```  
  
### 2. 连板梯队标签页组件（LimitUpTiers.vue）  
```vue  
<template>  
<div class="limit-up-tiers-container">  
<!-- 标签页 -->  
<el-tabs  
v-model="activeTier"  
@tab-change="handleTabChange"  
type="card"  
>  
<el-tab-pane  
v-for="item in tierOptions"  
:key="item.value"  
:label="item.label"  
>  
<!-- 连板股票列表 -->  
<el-table  
:data="stockList"  
border  
stripe  
v-loading="loading"  
>  
<el-table-column  
prop="stockName"  
label="股票名称"  
min-width="120"  
/>  
<el-table-column  
prop="stockCode"  
label="股票代码"  
width="100"  
/>  
<el-table-column  
prop="boardNum"  
label="连板数"  
width="100"  
/>  
<el-table-column  
prop="riseRate"  
label="涨跌幅(%)"  
width="100"  
>  
<template #default="scope">  
<span :class="scope.row.riseRate >= 0 ? 'text-red' : 'text-green'">  
{{ scope.row.riseRate.toFixed(2) }}  
</span>  
</template>  
</el-table-column>  
<el-table-column  
prop="orderAmount"  
label="封单额(万)"  
width="120"  
/>  
<el-table-column  
label="状态"  
width="100"  
>  
<template #default="scope">  
<el-tag  
:type="scope.row.status === '涨停' ? 'danger' : 'success'"  
size="small"  
>  
{{ scope.row.status }}  
</el-tag>  
</template>  
</el-table-column>  
</el-table>  
</el-tab-pane>  
</el-tabs>  
</div>  
</template>  
  
<script setup>  
import { ref, onMounted } from 'vue';  
import request from '@/utils/request';  
  
// 响应式数据  
const loading = ref(false);  
const stockList = ref([]);  
const activeTier = ref('1'); // 默认选中1板  
  
// 连板梯队选项  
const tierOptions = [  
{ label: '1板', value: '1' },  
{ label: '2板', value: '2' },  
{ label: '3板+', value: '3' }  
];  
  
// 获取连板梯队数据  
const getLimitUpData = async () => {  
loading.value = true;  
try {  
const res = await request.get('/stock/limit-up', {  
tier: activeTier.value  
});  
stockList.value = res.data.list;  
} catch (err) {  
console.error('获取连板梯队数据失败：', err);  
} finally {  
loading.value = false;  
}  
};  
  
// 标签页切换  
const handleTabChange = (tier) => {  
activeTier.value = tier;  
getLimitUpData();  
};  
  
// 初始化加载数据  
onMounted(() => {  
getLimitUpData();  
});  
</script>  
  
<style scoped>  
.limit-up-tiers-container {  
padding: 20px;  
background: #fff;  
border-radius: 8px;  
}  
  
.text-red {  
color: #f56c6c;  
}  
  
.text-green {  
color: #67c23a;  
}  
  
.el-tabs {  
--el-tabs-card-border-color: #e5e7eb;  
--el-tabs-active-color: #409eff;  
}  
</style>  
```  
  
## 三、React18 + Ant Design 组件模板  
### 1. 题材轮动表格组件（ThemeRotation.jsx）  
```jsx  
import React, { useState, useEffect } from 'react';  
import { Table, Button, Space, Tag, Pagination, Spin, message } from 'antd';  
import { useNavigate } from 'react-router-dom';  
import request from '@/utils/request';  
import './ThemeRotation.less';  
  
const ThemeRotation = () => {  
const navigate = useNavigate();  
  
// 状态管理  
const [loading, setLoading] = useState(false);  
const [themeList, setThemeList] = useState([]);  
const [total, setTotal] = useState(0);  
const [pageNum, setPageNum] = useState(1);  
const [pageSize, setPageSize] = useState(10);  
const [activeSort, setActiveSort] = useState('riseRate');  
  
// 排序选项  
const sortOptions = [  
{ label: '按涨幅排序', value: 'riseRate' },  
{ label: '按连板数排序', value: 'boardNum' },  
{ label: '按热度排序', value: 'hotValue' }  
];  
  
// 获取题材轮动数据  
const getThemeRotationData = async () => {  
setLoading(true);  
try {  
const res = await request.get('/theme/rotation', {  
pageNum,  
pageSize,  
sortType: activeSort  
});  
setThemeList(res.data.list);  
setTotal(res.data.total);  
} catch (err) {  
message.error('获取题材轮动数据失败');  
console.error('获取题材轮动数据失败：', err);  
} finally {  
setLoading(false);  
}  
};  
  
// 排序切换  
const handleSortChange = (sortType) => {  
setActiveSort(sortType);  
setPageNum(1); // 重置页码  
getThemeRotationData();  
};  
  
// 分页变化  
const handlePageChange = (current, size) => {  
setPageNum(current);  
setPageSize(size);  
getThemeRotationData();  
};  
  
// 查看详情  
const viewDetail = (record) => {  
navigate('/theme/detail', {  
search: `?themeId=${record.themeId}`  
});  
};  
  
// 表格列配置  
const columns = [  
{  
title: '题材名称',  
dataIndex: 'themeName',  
key: 'themeName',  
width: 150  
},  
{  
title: '涨幅(%)',  
dataIndex: 'riseRate',  
key: 'riseRate',  
width: 100,  
render: (text) => (  
<span className={text >= 0 ? 'text-red' : 'text-green'}>  
{text.toFixed(2)}  
</span>  
)  
},  
{  
title: '连板数',  
dataIndex: 'boardNum',  
key: 'boardNum',  
width: 100  
},  
{  
title: '热度值',  
dataIndex: 'hotValue',  
key: 'hotValue',  
width: 100  
},  
{  
title: '操作',  
key: 'action',  
width: 100,  
render: (_, record) => (  
<Button type="text" onClick={() => viewDetail(record)}>  
详情  
</Button>  
)  
}  
];  
  
// 初始化加载  
useEffect(() => {  
getThemeRotationData();  
}, [pageNum, pageSize, activeSort]);  
  
return (  
<div className="theme-rotation-container">  
{/* 筛选栏 */}  
<div className="filter-bar">  
<Space>  
{sortOptions.map(item => (  
<Button  
key={item.value}  
type={activeSort === item.value ? 'primary' : 'default'}  
onClick={() => handleSortChange(item.value)}  
>  
{item.label}  
</Button>  
))}  
</Space>  
</div>  
  
{/* 表格 */}  
<Spin spinning={loading} tip="数据加载中...">  
<Table  
columns={columns}  
dataSource={themeList}  
bordered  
rowKey="themeId"  
pagination={false}  
onRow={(record) => ({  
onClick: () => viewDetail(record)  
})}  
/>  
</Spin>  
  
{/* 分页 */}  
<div className="pagination">  
<Pagination  
current={pageNum}  
pageSize={pageSize}  
total={total}  
onChange={handlePageChange}  
onShowSizeChange={handlePageChange}  
showSizeChanger  
showTotal={(total) => `共 ${total} 条数据`}  
/>  
</div>  
</div>  
);  
};  
  
export default ThemeRotation;  
```  
  
### 2. 连板梯队标签页组件（LimitUpTiers.jsx）  
```jsx  
import React, { useState, useEffect } from 'react';  
import { Tabs, Table, Tag, Spin, message } from 'antd';  
import request from '@/utils/request';  
import './LimitUpTiers.less';  
  
const { TabPane } = Tabs;  
  
const LimitUpTiers = () => {  
// 状态管理  
const [loading, setLoading] = useState(false);  
const [stockList, setStockList] = useState([]);  
const [activeTier, setActiveTier] = useState('1');  
  
// 梯队选项  
const tierOptions = [  
{ label: '1板', value: '1' },  
{ label: '2板', value: '2' },  
{ label: '3板+', value: '3' }  
];  
  
// 获取连板数据  
const getLimitUpData = async () => {  
setLoading(true);  
try {  
const res = await request.get('/stock/limit-up', {  
tier: activeTier  
});  
setStockList(res.data.list);  
} catch (err) {  
message.error('获取连板梯队数据失败');  
console.error('获取连板梯队数据失败：', err);  
} finally {  
setLoading(false);  
}  
};  
  
// 标签页切换  
const handleTabChange = (tier) => {  
setActiveTier(tier);  
getLimitUpData();  
};  
  
// 表格列配置  
const columns = [  
{  
title: '股票名称',  
dataIndex: 'stockName',  
key: 'stockName',  
width: 120  
},  
{  
title: '股票代码',  
dataIndex: 'stockCode',  
key: 'stockCode',  
width: 100  
},  
{  
title: '连板数',  
dataIndex: 'boardNum',  
key: 'boardNum',  
width: 100  
},  
{  
title: '涨跌幅(%)',  
dataIndex: 'riseRate',  
key: 'riseRate',  
width: 100,  
render: (text) => (  
<span className={text >= 0 ? 'text-red' : 'text-green'}>  
{text.toFixed(2)}  
</span>  
)  
},  
{  
title: '封单额(万)',  
dataIndex: 'orderAmount',  
key: 'orderAmount',  
width: 120  
},  
{  
title: '状态',  
key: 'status',  
width: 100,  
render: (_, record) => (  
<Tag color={record.status === '涨停' ? 'red' : 'green'}>  
{record.status}  
</Tag>  
)  
}  
];  
  
// 初始化加载  
useEffect(() => {  
getLimitUpData();  
}, [activeTier]);  
  
return (  
<div className="limit-up-tiers-container">  
<Spin spinning={loading} tip="数据加载中...">  
<Tabs  
activeKey={activeTier}  
onChange={handleTabChange}  
type="card"  
>  
{tierOptions.map(item => (  
<TabPane tab={item.label} key={item.value}>  
<Table  
columns={columns}  
dataSource={stockList}  
bordered  
rowKey="stockCode"  
pagination={false}  
/>  
</TabPane>  
))}  
</Tabs>  
</Spin>  
</div>  
);  
};  
  
export default LimitUpTiers;  
```  
  
---  
  
### 总结  
1. **Axios 封装核心**：统一处理请求头、token、加载状态、错误提示，降低重复代码，提高项目可维护性；  
2. **Vue3 组件特点**：使用 Composition API 组织逻辑，结合 Element Plus 实现表格/标签页，响应式数据驱动视图；  
3. **React 组件特点**：使用 Hooks（useState/useEffect）管理状态，结合 Ant Design 组件库，逻辑与视图分离更清晰；  
4. **通用要点**：所有组件都包含 loading 状态、错误处理、数据渲染、交互逻辑，符合前端开发最佳实践。  
  
你可以直接复制这些代码到项目中使用，只需根据实际后端接口调整请求参数和返回字段即可。如果需要调整样式、补充更多交互逻辑（如筛选、搜索），可以告诉我具体需求。