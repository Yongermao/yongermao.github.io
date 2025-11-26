<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>招标文件检查流程清单 最终版</title>
<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.5.1/css/all.min.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.5.1/css/v4-shims.min.css">
<script>
tailwind.config = {
theme: {
extend: {
colors: {
primary: '#165DFF',
success: '#00B42A',
warning: '#FF7D00',
danger: '#F53F3F',
gray: {
50: '#F7F8FA',
100: '#F2F3F5',
200: '#E5E6EB',
300: '#C9CDD4',
400: '#86909C',
500: '#4E5969',
600: '#272E3B',
700: '#1D2129',
}
},
fontFamily: {
inter: ['Inter', 'system-ui', 'sans-serif'],
},
},
}
}
</script>
<style type="text/tailwindcss">
@layer utilities {
.content-auto {
content-visibility: auto;
}
.checklist-item {
@apply flex items-center justify-between p-3 sm:p-4 mb-2 sm:mb-3 rounded-lg transition-all duration-300 ease-in-out;
}
.checklist-item-pending {
@apply bg-white border border-danger/30 shadow-sm hover:shadow-md;
}
.checklist-item-completed {
@apply bg-gray-50 border border-gray-200 shadow-sm;
}
.checklist-text-pending {
@apply text-danger font-medium text-sm sm:text-base;
}
.checklist-text-completed {
@apply text-gray-400 line-through text-sm sm:text-base;
}
.check-icon {
@apply w-6 h-6 rounded-full flex items-center justify-center transition-all duration-300 cursor-pointer;
}
.check-icon-pending {
@apply border-2 border-danger/50 text-danger hover:bg-danger/10;
}
.check-icon-completed {
@apply bg-success text-white;
}
.project-card {
@apply bg-white rounded-xl shadow-sm border border-gray-100 overflow-hidden transition-all duration-300 hover:shadow-md;
}
.project-header {
@apply p-3 sm:p-4 cursor-pointer flex items-center justify-between;
}
.project-content {
@apply p-3 sm:p-4 border-t border-gray-100;
}
.history-item {
@apply p-3 border-b border-gray-100 hover:bg-gray-50 transition-colors cursor-pointer;
}
.tab-button {
@apply px-4 sm:px-6 py-2 sm:py-3 rounded-t-lg font-medium transition-all duration-300 cursor-pointer text-sm sm:text-base;
}
.tab-button-active {
@apply bg-white text-primary border-b-2 border-primary shadow-sm;
}
.tab-button-inactive {
@apply bg-gray-100 text-gray-500 hover:bg-gray-200;
}
.tab-content {
@apply bg-white p-4 sm:p-6 border border-gray-200 border-t-0 rounded-b-lg;
}
/* 响应式工具类 */
.mobile-hide {
@apply hidden sm:block;
}
.mobile-show {
@apply block sm:hidden;
}
}
</style>
</head>
<body class="bg-gray-50 font-inter min-h-screen">
<!-- 顶部导航 -->
<nav class="bg-white shadow-sm sticky top-0 z-10">
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
<div class="flex justify-between h-14 sm:h-16">
<div class="flex items-center">
<i class="fa fa-file-text-o text-primary text-xl sm:text-2xl mr-2 sm:mr-3"></i>
<h1 class="text-base sm:text-xl font-bold text-gray-700">招标文件检查流程清单</h1>
</div>
<div class="flex items-center space-x-2 sm:space-x-4">
<button id="saveProjectBtn" class="px-3 sm:px-4 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors flex items-center space-x-1 sm:space-x-2 text-sm">
<i class="fa fa-save"></i>
<span class="mobile-hide">保存项目</span>
<span class="mobile-show">保存</span>
</button>
<button id="historyBtn" class="px-3 sm:px-4 py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors flex items-center space-x-1 sm:space-x-2 text-sm">
<i class="fa fa-history"></i>
<span class="mobile-hide">历史记录</span>
<span class="mobile-show">历史</span>
</button>
<button id="themeToggle" class="p-2 rounded-full hover:bg-gray-100 transition-colors">
<i class="fa fa-moon-o text-gray-500"></i>
</button>
</div>
</div>
</div>
</nav>
<!-- 主内容区 -->
<main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-4 sm:py-8">
<!-- 项目信息 -->
<div class="bg-white rounded-xl shadow-sm p-4 sm:p-6 mb-4 sm:mb-8 border border-gray-100">
<h2 class="text-base sm:text-lg font-semibold text-gray-700 mb-3 sm:mb-4">项目信息</h2>
<div class="grid grid-cols-1 sm:grid-cols-2 gap-3 sm:gap-6">
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">项目名称 <span class="text-danger">*</span></label>
<input
type="text"
id="projectName"
placeholder="请输入项目名称..."
class="w-full px-3 sm:px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-primary outline-none transition-all text-sm"
>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">创建日期</label>
<input
type="text"
id="projectDate"
value=""
readonly
class="w-full px-3 sm:px-4 py-2 border border-gray-300 rounded-lg bg-gray-50 text-gray-500 text-sm"
>
</div>
</div>
</div>
<!-- 文档类型选择 - 默认隐藏，输入项目名称后显示 -->
<div id="documentTypeTabs" class="hidden mb-4 sm:mb-8">
<div class="flex border-b border-gray-200">
<div
id="bidDocumentTab"
class="tab-button tab-button-active"
onclick="switchDocumentType('bidDocument')"
>
<i class="fa fa-file-text-o mr-1 sm:mr-2"></i>招标文件
</div>
<div
id="winningAnnouncementTab"
class="tab-button tab-button-inactive"
onclick="switchDocumentType('winningAnnouncement')"
>
<i class="fa fa-bullhorn mr-1 sm:mr-2"></i>中标公告
</div>
</div>
</div>
<!-- 统计卡片 - 默认隐藏，选择文档类型后显示 -->
<div id="statsContainer" class="hidden grid grid-cols-1 sm:grid-cols-3 gap-3 sm:gap-6 mb-4 sm:mb-8">
<div class="bg-white rounded-xl shadow-sm p-3 sm:p-6 border border-gray-100">
<div class="flex items-center justify-between">
<div>
<p class="text-xs sm:text-sm font-medium text-gray-500">总检查项</p>
<p id="totalItems" class="text-lg sm:text-2xl font-bold text-gray-700">0</p>
</div>
<div class="w-8 sm:w-12 h-8 sm:h-12 bg-primary/10 rounded-full flex items-center justify-center">
<i class="fa fa-list text-primary text-sm sm:text-xl"></i>
</div>
</div>
</div>
<div class="bg-white rounded-xl shadow-sm p-3 sm:p-6 border border-gray-100">
<div class="flex items-center justify-between">
<div>
<p class="text-xs sm:text-sm font-medium text-gray-500">已完成</p>
<p id="completedItems" class="text-lg sm:text-2xl font-bold text-success">0</p>
</div>
<div class="w-8 sm:w-12 h-8 sm:h-12 bg-success/10 rounded-full flex items-center justify-center">
<i class="fa fa-check text-success text-sm sm:text-xl"></i>
</div>
</div>
</div>
<div class="bg-white rounded-xl shadow-sm p-3 sm:p-6 border border-gray-100">
<div class="flex items-center justify-between">
<div>
<p class="text-xs sm:text-sm font-medium text-gray-500">待检查</p>
<p id="pendingItems" class="text-lg sm:text-2xl font-bold text-danger">0</p>
</div>
<div class="w-8 sm:w-12 h-8 sm:h-12 bg-danger/10 rounded-full flex items-center justify-center">
<i class="fa fa-exclamation-triangle text-danger text-sm sm:text-xl"></i>
</div>
</div>
</div>
</div>
<!-- 添加新项目表单 - 默认隐藏，选择文档类型后显示 -->
<div id="addItemForm" class="hidden bg-white rounded-xl shadow-sm p-3 sm:p-6 mb-4 sm:mb-8 border border-gray-100">
<h2 class="text-base sm:text-lg font-semibold text-gray-700 mb-3 sm:mb-4">添加检查项目</h2>
<div class="flex space-x-2 sm:space-x-4">
<input
type="text"
id="newItemInput"
placeholder="输入检查项目名称..."
class="flex-1 px-3 sm:px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-primary focus:border-primary outline-none transition-all text-sm"
>
<button
id="addItemBtn"
class="px-4 sm:px-6 py-2 bg-primary text-white rounded-lg hover:bg-primary/90 transition-colors flex items-center space-x-1 sm:space-x-2 text-sm"
>
<i class="fa fa-plus"></i>
<span>添加</span>
</button>
</div>
</div>
<!-- 当前项目检查清单 - 默认隐藏，选择文档类型后显示 -->
<div id="checklistContainer" class="hidden bg-white rounded-xl shadow-sm border border-gray-100 mb-4 sm:mb-8">
<!-- 招标文件检查内容 -->
<div id="bidDocumentContent" class="tab-content">
<div class="flex items-center justify-between mb-3 sm:mb-6">
<h2 class="text-base sm:text-lg font-semibold text-gray-700">招标文件检查清单</h2>
<div class="flex space-x-1 sm:space-x-2">
<button id="clearCompletedBtn" class="px-2 sm:px-4 py-1 sm:py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors text-xs sm:text-sm">
<i class="fa fa-trash-o mr-1"></i>清除已完成
</button>
<button id="clearAllBtn" class="px-2 sm:px-4 py-1 sm:py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors text-xs sm:text-sm">
<i class="fa fa-broom mr-1"></i>清空全部
</button>
</div>
</div>
<!-- 空状态提示 -->
<div id="bidDocumentEmptyState" class="text-center py-8 sm:py-12">
<div class="w-12 sm:w-16 h-12 sm:h-16 bg-gray-100 rounded-full mx-auto mb-3 sm:mb-4 flex items-center justify-center">
<i class="fa fa-file-text-o text-gray-400 text-lg sm:text-2xl"></i>
</div>
<p class="text-gray-500 text-sm sm:text-base">暂无招标文件检查项目</p>
<p class="text-gray-400 text-xs sm:text-sm mt-2">请在上方添加检查项目开始使用</p>
</div>
<!-- 清单容器 -->
<div id="bidDocumentList" class="space-y-1 sm:space-y-2">
<!-- 检查项将通过JS动态添加 -->
</div>
</div>
<!-- 中标公告检查内容 -->
<div id="winningAnnouncementContent" class="tab-content hidden">
<div class="flex items-center justify-between mb-3 sm:mb-6">
<h2 class="text-base sm:text-lg font-semibold text-gray-700">中标（候选人）公告检查清单</h2>
<div class="flex space-x-1 sm:space-x-2">
<button id="clearWinningCompletedBtn" class="px-2 sm:px-4 py-1 sm:py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors text-xs sm:text-sm">
<i class="fa fa-trash-o mr-1"></i>清除已完成
</button>
<button id="clearWinningAllBtn" class="px-2 sm:px-4 py-1 sm:py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors text-xs sm:text-sm">
<i class="fa fa-broom mr-1"></i>清空全部
</button>
</div>
</div>
<!-- 空状态提示 -->
<div id="winningAnnouncementEmptyState" class="text-center py-8 sm:py-12">
<div class="w-12 sm:w-16 h-12 sm:h-16 bg-gray-100 rounded-full mx-auto mb-3 sm:mb-4 flex items-center justify-center">
<i class="fa fa-bullhorn text-gray-400 text-lg sm:text-2xl"></i>
</div>
<p class="text-gray-500 text-sm sm:text-base">暂无中标公告检查项目</p>
<p class="text-gray-400 text-xs sm:text-sm mt-2">请在上方添加检查项目开始使用</p>
</div>
<!-- 清单容器 -->
<div id="winningAnnouncementList" class="space-y-1 sm:space-y-2">
<!-- 检查项将通过JS动态添加 -->
</div>
</div>
</div>
<!-- 历史项目列表 -->
<div class="bg-white rounded-xl shadow-sm border border-gray-100 mb-4 sm:mb-8">
<div class="project-header" onclick="toggleProject('historyProjects')">
<div class="flex items-center space-x-2">
<i class="fa fa-history text-warning"></i>
<h2 class="text-base sm:text-lg font-semibold text-gray-700">历史项目记录</h2>
</div>
<i class="fa fa-chevron-down text-gray-400 transition-transform duration-300" id="historyProjectsArrow"></i>
</div>
<div class="project-content hidden" id="historyProjectsContent">
<div id="historyList" class="max-h-64 sm:max-h-96 overflow-y-auto">
<!-- 历史项目将通过JS动态添加 -->
<div class="text-center py-6 sm:py-8 text-gray-500 text-sm" id="emptyHistory">
暂无历史项目记录
</div>
</div>
</div>
</div>
</main>
<!-- 页脚 -->
<footer class="bg-white border-t border-gray-200 py-4 sm:py-6 mt-6 sm:mt-12">
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center text-gray-500 text-xs sm:text-sm">
<p>© 2025 招标文件检查流程清单 | 专业的文档检查工具</p>
</div>
</footer>
<!-- 历史记录模态框 -->
<div id="historyModal" class="fixed inset-0 bg-black/50 z-50 hidden flex items-center justify-center p-3 sm:p-4">
<div class="bg-white rounded-xl shadow-xl w-full max-w-sm sm:max-w-2xl max-h-[90vh] overflow-hidden">
<div class="p-4 sm:p-6 border-b border-gray-200 flex justify-between items-center">
<h3 class="text-base sm:text-xl font-bold text-gray-700">历史项目记录</h3>
<button onclick="closeHistoryModal()" class="text-gray-400 hover:text-gray-600">
<i class="fa fa-times text-lg sm:text-xl"></i>
</button>
</div>
<div class="p-3 sm:p-6 max-h-[calc(90vh-100px)] overflow-y-auto">
<div id="modalHistoryList" class="space-y-2 sm:space-y-3">
<!-- 历史项目将通过JS动态添加 -->
<div class="text-center py-6 sm:py-8 text-gray-500 text-sm" id="emptyModalHistory">
暂无历史项目记录
</div>
</div>
</div>
</div>
</div>
<script>
// 全局变量
let currentProject = {
id: Date.now(),
name: '',
date: new Date().toLocaleDateString(),
bidDocumentItems: [],
winningAnnouncementItems: [],
createdAt: new Date().toISOString(),
currentDocumentType: 'bidDocument'
};
let historyProjects = [];
let darkMode = false;
// 默认招标文件检查项目列表
const defaultBidDocumentItems = [
"采购内容（服务或交货期、质保期、质量要求等）",
"是否面向中小",
"特定资格要求",
"文件获取时间",
"开标时间及地址",
"发布媒介",
"招标采购人信息（单位名称、地址、联系人及电话）",
"投标人须知前附表中与上述内容是否一致",
"标段划分、标段号或名称及各标段控制价",
"投标保证金",
"履约保证金",
"支付方式",
"文件密封要求",
"投标人须知前附表内同是否与正文内容及序号保持一致",
"形式评审内容与投标人前附表是否一致",
"资格评审内容与投标人前附表是否一致",
"响应性评审内容与投标人前附表是否一致",
"分值是否是100分",
"分项（报价、技术、综合或商务）分值是否和分值分布一致",
"报价分计算方式和分值是否正确",
"技术部分分值合计是否与分值分布一致",
"技术部分各单项打分里的每一条描述和分值是否正确",
"综合或商务部分分值合计是否与分值分布一致",
"综合或商务部分各单项打分里的每一条描述和分值是否正确",
"技术参数是否合理合规",
"技术参数数量是否和技术分对应",
"合同条款是否合适",
"支付方式是否与前附表一致",
"投标文件格式目录与内容是否一致",
"投标函和附录内容是否一致，且与投标人须知前附表、公告内容保持一致",
"资格审查资料是否和投标人须知前附表及公告要求保持一致",
"中小企业声明函内容是否和项目属性（货物、工程、服务）一致"
];
// 默认中标（候选人）公告检查项目列表
const defaultWinningAnnouncementItems = [
"项目编号",
"预算金额",
"招标公告发布日期",
"开标日期",
"开标地点",
"中标单位名称",
"中标单位地址",
"中标金额",
"服务期限（交货期）",
"质保期",
"质量标准",
"排序及得分",
"代理费标准及金额",
"发布媒介",
"招标人及代理机构信息"
];
// DOM元素
const projectNameInput = document.getElementById('projectName');
const projectDateInput = document.getElementById('projectDate');
const newItemInput = document.getElementById('newItemInput');
const addItemBtn = document.getElementById('addItemBtn');
const documentTypeTabs = document.getElementById('documentTypeTabs');
const statsContainer = document.getElementById('statsContainer');
const addItemForm = document.getElementById('addItemForm');
const checklistContainer = document.getElementById('checklistContainer');
const bidDocumentTab = document.getElementById('bidDocumentTab');
const winningAnnouncementTab = document.getElementById('winningAnnouncementTab');
const bidDocumentContent = document.getElementById('bidDocumentContent');
const winningAnnouncementContent = document.getElementById('winningAnnouncementContent');
const bidDocumentEmptyState = document.getElementById('bidDocumentEmptyState');
const winningAnnouncementEmptyState = document.getElementById('winningAnnouncementEmptyState');
const bidDocumentList = document.getElementById('bidDocumentList');
const winningAnnouncementList = document.getElementById('winningAnnouncementList');
const totalItemsElement = document.getElementById('totalItems');
const completedItemsElement = document.getElementById('completedItems');
const pendingItemsElement = document.getElementById('pendingItems');
const saveProjectBtn = document.getElementById('saveProjectBtn');
const historyBtn = document.getElementById('historyBtn');
const themeToggle = document.getElementById('themeToggle');
const historyModal = document.getElementById('historyModal');
const modalHistoryList = document.getElementById('modalHistoryList');
const emptyModalHistory = document.getElementById('emptyModalHistory');
const historyList = document.getElementById('historyList');
const emptyHistory = document.getElementById('emptyHistory');
const clearCompletedBtn = document.getElementById('clearCompletedBtn');
const clearAllBtn = document.getElementById('clearAllBtn');
const clearWinningCompletedBtn = document.getElementById('clearWinningCompletedBtn');
const clearWinningAllBtn = document.getElementById('clearWinningAllBtn');
// 初始化
function init() {
console.log('初始化应用...');
// 设置当前日期
projectDateInput.value = new Date().toLocaleDateString();
// 加载历史记录
loadHistoryProjects();
// 事件监听
addItemBtn.addEventListener('click', addNewItem);
newItemInput.addEventListener('keypress', (e) => {
if (e.key === 'Enter') addNewItem();
});
saveProjectBtn.addEventListener('click', saveCurrentProject);
historyBtn.addEventListener('click', openHistoryModal);
themeToggle.addEventListener('click', toggleTheme);
projectNameInput.addEventListener('input', handleProjectNameInput);
clearCompletedBtn.addEventListener('click', () => clearCompletedItems('bidDocument'));
clearAllBtn.addEventListener('click', () => clearAllItems('bidDocument'));
clearWinningCompletedBtn.addEventListener('click', () => clearCompletedItems('winningAnnouncement'));
clearWinningAllBtn.addEventListener('click', () => clearAllItems('winningAnnouncement'));
// 初始化统计
updateStats();
console.log('应用初始化完成');
}
// 处理项目名称输入
function handleProjectNameInput() {
const projectName = projectNameInput.value.trim();
currentProject.name = projectName;
console.log('项目名称输入:', projectName);
if (projectName) {
// 显示文档类型选择和相关内容
documentTypeTabs.classList.remove('hidden');
statsContainer.classList.remove('hidden');
addItemForm.classList.remove('hidden');
checklistContainer.classList.remove('hidden');
// 如果是首次输入项目名称，添加默认检查项目
if (currentProject.bidDocumentItems.length === 0) {
console.log('添加默认招标文件检查项目');
addDefaultBidDocumentItems();
}
if (currentProject.winningAnnouncementItems.length === 0) {
console.log('添加默认中标公告检查项目');
addDefaultWinningAnnouncementItems();
}
} else {
// 隐藏所有内容
documentTypeTabs.classList.add('hidden');
statsContainer.classList.add('hidden');
addItemForm.classList.add('hidden');
checklistContainer.classList.add('hidden');
}
}
// 添加默认招标文件检查项目
function addDefaultBidDocumentItems() {
defaultBidDocumentItems.forEach(text => {
const newItem = {
id: Date.now() + Math.random(),
text: text,
completed: false,
createdAt: new Date().toISOString()
};
currentProject.bidDocumentItems.push(newItem);
});
renderChecklist('bidDocument');
updateStats();
console.log('已添加', defaultBidDocumentItems.length, '个招标文件检查项目');
}
// 添加默认中标公告检查项目
function addDefaultWinningAnnouncementItems() {
defaultWinningAnnouncementItems.forEach(text => {
const newItem = {
id: Date.now() + Math.random() + 1000,
text: text,
completed: false,
createdAt: new Date().toISOString()
};
currentProject.winningAnnouncementItems.push(newItem);
});
renderChecklist('winningAnnouncement');
// 切换回当前文档类型
switchDocumentType(currentProject.currentDocumentType);
console.log('已添加', defaultWinningAnnouncementItems.length, '个中标公告检查项目');
}
// 切换文档类型
function switchDocumentType(documentType) {
currentProject.currentDocumentType = documentType;
console.log('切换文档类型:', documentType);
// 更新标签样式
if (documentType === 'bidDocument') {
bidDocumentTab.classList.remove('tab-button-inactive');
bidDocumentTab.classList.add('tab-button-active');
winningAnnouncementTab.classList.remove('tab-button-active');
winningAnnouncementTab.classList.add('tab-button-inactive');
bidDocumentContent.classList.remove('hidden');
winningAnnouncementContent.classList.add('hidden');
} else {
bidDocumentTab.classList.remove('tab-button-active');
bidDocumentTab.classList.add('tab-button-inactive');
winningAnnouncementTab.classList.remove('tab-button-inactive');
winningAnnouncementTab.classList.add('tab-button-active');
bidDocumentContent.classList.add('hidden');
winningAnnouncementContent.classList.remove('hidden');
}
updateStats();
}
// 添加新项目
function addNewItem() {
const itemText = newItemInput.value.trim();
if (itemText) {
const newItem = {
id: Date.now(),
text: itemText,
completed: false,
createdAt: new Date().toISOString()
};
if (currentProject.currentDocumentType === 'bidDocument') {
currentProject.bidDocumentItems.push(newItem);
renderChecklist('bidDocument');
} else {
currentProject.winningAnnouncementItems.push(newItem);
renderChecklist('winningAnnouncement');
}
newItemInput.value = '';
updateStats();
console.log('添加新项目:', itemText);
// 添加动画效果
const newItemElement = document.querySelector(`[data-id="${newItem.id}"]`);
if (newItemElement) {
newItemElement.classList.add('animate-pulse');
setTimeout(() => {
newItemElement.classList.remove('animate-pulse');
}, 1000);
}
}
}
// 切换项目完成状态
function toggleItemCompleted(itemId, documentType) {
console.log('切换项目完成状态:', itemId, documentType);
let items = documentType === 'bidDocument' ? currentProject.bidDocumentItems : currentProject.winningAnnouncementItems;
const item = items.find(item => item.id === itemId);
if (item) {
item.completed = !item.completed;
renderChecklist(documentType);
updateStats();
console.log('项目状态已更新:', item.text, '->', item.completed);
}
}
// 删除项目
function deleteItem(itemId, documentType) {
console.log('删除项目:', itemId, documentType);
if (documentType === 'bidDocument') {
currentProject.bidDocumentItems = currentProject.bidDocumentItems.filter(item => item.id !== itemId);
renderChecklist('bidDocument');
} else {
currentProject.winningAnnouncementItems = currentProject.winningAnnouncementItems.filter(item => item.id !== itemId);
renderChecklist('winningAnnouncement');
}
updateStats();
console.log('项目已删除');
}
// 清除已完成项目
function clearCompletedItems(documentType) {
console.log('清除已完成项目:', documentType);
if (documentType === 'bidDocument') {
currentProject.bidDocumentItems = currentProject.bidDocumentItems.filter(item => !item.completed);
renderChecklist('bidDocument');
} else {
currentProject.winningAnnouncementItems = currentProject.winningAnnouncementItems.filter(item => !item.completed);
renderChecklist('winningAnnouncement');
}
updateStats();
console.log('已完成项目已清除');
}
// 清空所有项目
function clearAllItems(documentType) {
if (confirm('确定要清空所有检查项目吗？')) {
console.log('清空所有项目:', documentType);
if (documentType === 'bidDocument') {
currentProject.bidDocumentItems = [];
renderChecklist('bidDocument');
} else {
currentProject.winningAnnouncementItems = [];
renderChecklist('winningAnnouncement');
}
updateStats();
console.log('所有项目已清空');
}
}
// 保存当前项目到历史记录
function saveCurrentProject() {
const projectName = projectNameInput.value.trim();
if (!projectName) {
alert('请输入项目名称');
projectNameInput.focus();
return;
}
// 更新当前项目信息
currentProject.name = projectName;
currentProject.date = projectDateInput.value;
currentProject.updatedAt = new Date().toISOString();
console.log('保存项目:', currentProject.name);
// 检查是否已存在同名项目
const existingIndex = historyProjects.findIndex(p => p.name === projectName);
if (existingIndex >= 0) {
if (confirm('已存在同名项目，是否覆盖？')) {
historyProjects[existingIndex] = {...currentProject};
console.log('项目已覆盖');
} else {
return;
}
} else {
// 添加新项目
historyProjects.push({...currentProject});
console.log('项目已添加到历史记录');
}
// 保存到本地存储
saveHistoryProjects();
// 显示成功提示
alert('项目已成功保存到历史记录');
// 更新历史记录显示
renderHistoryList();
}
// 加载历史项目
function loadProject(projectId) {
console.log('加载历史项目:', projectId);
const project = historyProjects.find(p => p.id === projectId);
if (project) {
console.log('找到项目:', project.name);
// 保存当前项目（如果有内容）
if ((currentProject.bidDocumentItems.length > 0 || currentProject.winningAnnouncementItems.length > 0) || currentProject.name) {
const tempProject = {...currentProject};
tempProject.id = Date.now();
tempProject.name = tempProject.name || '未命名项目';
tempProject.updatedAt = new Date().toISOString();
// 检查是否已存在
const existingIndex = historyProjects.findIndex(p => p.name === tempProject.name);
if (existingIndex === -1) {
historyProjects.push(tempProject);
saveHistoryProjects();
console.log('临时项目已保存');
}
}
// 加载选中的项目
currentProject = {...project};
projectNameInput.value = currentProject.name;
projectDateInput.value = currentProject.date;
// 显示所有内容
documentTypeTabs.classList.remove('hidden');
statsContainer.classList.remove('hidden');
addItemForm.classList.remove('hidden');
checklistContainer.classList.remove('hidden');
// 切换到项目的当前文档类型
switchDocumentType(currentProject.currentDocumentType || 'bidDocument');
// 渲染检查清单
renderChecklist('bidDocument');
renderChecklist('winningAnnouncement');
updateStats();
closeHistoryModal();
console.log('项目加载完成:', currentProject.name);
} else {
console.log('未找到项目:', projectId);
}
}
// 删除历史项目
function deleteHistoryProject(projectId) {
console.log('删除历史项目:', projectId);
if (confirm('确定要删除这个历史项目吗？')) {
historyProjects = historyProjects.filter(p => p.id !== projectId);
saveHistoryProjects();
renderHistoryList();
renderModalHistoryList();
console.log('项目已删除');
}
}
// 渲染检查清单
function renderChecklist(documentType) {
console.log('渲染检查清单:', documentType);
const listElement = documentType === 'bidDocument' ? bidDocumentList : winningAnnouncementList;
const emptyStateElement = documentType === 'bidDocument' ? bidDocumentEmptyState : winningAnnouncementEmptyState;
const items = documentType === 'bidDocument' ? currentProject.bidDocumentItems : currentProject.winningAnnouncementItems;
listElement.innerHTML = '';
if (items.length === 0) {
emptyStateElement.classList.remove('hidden');
console.log('检查清单为空:', documentType);
return;
}
emptyStateElement.classList.add('hidden');
// 按创建时间排序（新的在上面）
const sortedItems = [...items].sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
sortedItems.forEach(item => {
const itemElement = document.createElement('div');
itemElement.className = `checklist-item ${item.completed ? 'checklist-item-completed' : 'checklist-item-pending'}`;
itemElement.setAttribute('data-id', item.id);
itemElement.innerHTML = `
<div class="flex items-center space-x-2 sm:space-x-3 flex-1">
<div class="check-icon ${item.completed ? 'check-icon-completed' : 'check-icon-pending'}"
onclick="toggleItemCompleted(${item.id}, '${documentType}')">
${item.completed ? '<i class="fa fa-check"></i>' : ''}
</div>
<span class="${item.completed ? 'checklist-text-completed' : 'checklist-text-pending'}">
${item.text}
</span>
</div>
<button onclick="deleteItem(${item.id}, '${documentType}')" class="text-gray-400 hover:text-danger p-1 sm:p-2 rounded-full hover:bg-gray-100 transition-colors">
<i class="fa fa-trash-o text-xs sm:text-sm"></i>
</button>
`;
listElement.appendChild(itemElement);
});
console.log('已渲染', items.length, '个检查项目:', documentType);
}
// 渲染历史项目列表
function renderHistoryList() {
console.log('渲染历史项目列表');
historyList.innerHTML = '';
if (historyProjects.length === 0) {
emptyHistory.classList.remove('hidden');
console.log('历史项目列表为空');
return;
}
emptyHistory.classList.add('hidden');
// 按更新时间排序（新的在上面）
const sortedProjects = [...historyProjects].sort((a, b) => new Date(b.updatedAt || b.createdAt) - new Date(a.updatedAt || a.createdAt));
sortedProjects.forEach(project => {
const bidCompleted = project.bidDocumentItems ? project.bidDocumentItems.filter(item => item.completed).length : 0;
const bidTotal = project.bidDocumentItems ? project.bidDocumentItems.length : 0;
const winningCompleted = project.winningAnnouncementItems ? project.winningAnnouncementItems.filter(item => item.completed).length : 0;
const winningTotal = project.winningAnnouncementItems ? project.winningAnnouncementItems.length : 0;
const totalCompleted = bidCompleted + winningCompleted;
const totalItems = bidTotal + winningTotal;
const completionRate = totalItems > 0 ? Math.round((totalCompleted / totalItems) * 100) : 0;
const projectElement = document.createElement('div');
projectElement.className = 'history-item';
projectElement.innerHTML = `
<div class="flex justify-between items-center">
<div>
<h4 class="font-medium text-gray-700 text-sm">${project.name}</h4>
<p class="text-xs text-gray-500">${project.date} | ${totalCompleted}/${totalItems} 已完成</p>
<p class="text-xs text-gray-400 mt-1">
招标文件: ${bidCompleted}/${bidTotal} | 中标公告: ${winningCompleted}/${winningTotal}
</p>
</div>
<div class="flex space-x-1">
<button onclick="loadProject(${project.id})" class="text-primary hover:text-primary/80 p-1">
<i class="fa fa-folder-open text-sm"></i>
</button>
<button onclick="deleteHistoryProject(${project.id})" class="text-danger hover:text-danger/80 p-1">
<i class="fa fa-trash-o text-sm"></i>
</button>
</div>
</div>
<div class="mt-1 bg-gray-100 rounded-full h-1.5">
<div class="h-1.5 rounded-full ${completionRate === 100 ? 'bg-success' : completionRate > 0 ? 'bg-warning' : 'bg-danger'}"
style="width: ${completionRate}%"></div>
</div>
`;
historyList.appendChild(projectElement);
});
console.log('已渲染', historyProjects.length, '个历史项目');
}
// 渲染模态框历史项目列表
function renderModalHistoryList() {
console.log('渲染模态框历史项目列表');
modalHistoryList.innerHTML = '';
if (historyProjects.length === 0) {
emptyModalHistory.classList.remove('hidden');
console.log('模态框历史项目列表为空');
return;
}
emptyModalHistory.classList.add('hidden');
// 按更新时间排序（新的在上面）
const sortedProjects = [...historyProjects].sort((a, b) => new Date(b.updatedAt || b.createdAt) - new Date(a.updatedAt || a.createdAt));
sortedProjects.forEach(project => {
const bidCompleted = project.bidDocumentItems ? project.bidDocumentItems.filter(item => item.completed).length : 0;
const bidTotal = project.bidDocumentItems ? project.bidDocumentItems.length : 0;
const winningCompleted = project.winningAnnouncementItems ? project.winningAnnouncementItems.filter(item => item.completed).length : 0;
const winningTotal = project.winningAnnouncementItems ? project.winningAnnouncementItems.length : 0;
const totalCompleted = bidCompleted + winningCompleted;
const totalItems = bidTotal + winningTotal;
const completionRate = totalItems > 0 ? Math.round((totalCompleted / totalItems) * 100) : 0;
const projectElement = document.createElement('div');
projectElement.className = 'border rounded-lg p-3 hover:shadow-sm transition-shadow';
projectElement.innerHTML = `
<div class="flex justify-between items-start mb-2">
<div>
<h4 class="font-medium text-gray-700 text-sm">${project.name}</h4>
<p class="text-xs text-gray-500">${project.date}</p>
<p class="text-xs text-gray-400 mt-1">
招标文件: ${bidCompleted}/${bidTotal} | 中标公告: ${winningCompleted}/${winningTotal}
</p>
</div>
<div class="flex space-x-1">
<button onclick="loadProject(${project.id})" class="text-primary hover:text-primary/80 p-1">
<i class="fa fa-folder-open text-sm"></i>
</button>
<button onclick="deleteHistoryProject(${project.id})" class="text-danger hover:text-danger/80 p-1">
<i class="fa fa-trash-o text-sm"></i>
</button>
</div>
</div>
<div class="flex justify-between items-center text-xs text-gray-500 mb-2">
<span>完成度: ${completionRate}%</span>
<span>${totalCompleted}/${totalItems} 项</span>
</div>
<div class="bg-gray-100 rounded-full h-1.5">
<div class="h-1.5 rounded-full ${completionRate === 100 ? 'bg-success' : completionRate > 0 ? 'bg-warning' : 'bg-danger'}"
style="width: ${completionRate}%"></div>
</div>
`;
modalHistoryList.appendChild(projectElement);
});
console.log('已渲染', historyProjects.length, '个模态框历史项目');
}
// 更新统计信息
function updateStats() {
let items = currentProject.currentDocumentType === 'bidDocument'
? currentProject.bidDocumentItems
: currentProject.winningAnnouncementItems;
const total = items.length;
const completed = items.filter(item => item.completed).length;
const pending = total - completed;
totalItemsElement.textContent = total;
completedItemsElement.textContent = completed;
pendingItemsElement.textContent = pending;
console.log('更新统计:', currentProject.currentDocumentType, '| 总计:', total, '| 已完成:', completed, '| 待检查:', pending);
// 添加数字变化动画
[totalItemsElement, completedItemsElement, pendingItemsElement].forEach(element => {
element.classList.add('animate-pulse');
setTimeout(() => {
element.classList.remove('animate-pulse');
}, 500);
});
}
// 切换主题
function toggleTheme() {
darkMode = !darkMode;
document.body.classList.toggle('dark-mode');
const icon = themeToggle.querySelector('i');
if (darkMode) {
icon.classList.remove('fa-moon-o');
icon.classList.add('fa-sun-o');
document.body.classList.add('bg-gray-900');
document.body.classList.add('text-white');
} else {
icon.classList.remove('fa-sun-o');
icon.classList.add('fa-moon-o');
document.body.classList.remove('bg-gray-900');
document.body.classList.remove('text-white');
}
console.log('主题已切换:', darkMode ? '深色' : '浅色');
}
// 切换项目折叠状态
function toggleProject(projectId) {
const content = document.getElementById(`${projectId}Content`);
const arrow = document.getElementById(`${projectId}Arrow`);
content.classList.toggle('hidden');
arrow.classList.toggle('rotate-180');
console.log('项目折叠状态已切换:', projectId);
}
// 打开历史记录模态框
function openHistoryModal() {
renderModalHistoryList();
historyModal.classList.remove('hidden');
console.log('历史记录模态框已打开');
}
// 关闭历史记录模态框
function closeHistoryModal() {
historyModal.classList.add('hidden');
console.log('历史记录模态框已关闭');
}
// 保存历史项目到本地存储
function saveHistoryProjects() {
localStorage.setItem('checklistHistoryProjects', JSON.stringify(historyProjects));
console.log('历史项目已保存到本地存储:', historyProjects.length, '个项目');
}
// 从本地存储加载历史项目
function loadHistoryProjects() {
const savedProjects = localStorage.getItem('checklistHistoryProjects');
if (savedProjects) {
try {
historyProjects = JSON.parse(savedProjects);
renderHistoryList();
console.log('已从本地存储加载', historyProjects.length, '个历史项目');
} catch (e) {
console.error('加载历史项目失败:', e);
historyProjects = [];
}
} else {
console.log('本地存储中没有历史项目');
}
}
// 全局函数（供HTML调用）
window.toggleItemCompleted = toggleItemCompleted;
window.deleteItem = deleteItem;
window.toggleProject = toggleProject;
window.loadProject = loadProject;
window.deleteHistoryProject = deleteHistoryProject;
window.openHistoryModal = openHistoryModal;
window.closeHistoryModal = closeHistoryModal;
window.switchDocumentType = switchDocumentType;
// 初始化应用
document.addEventListener('DOMContentLoaded', init);
// 添加错误处理
window.addEventListener('error', function(event) {
console.error('全局错误:', event.error);
console.error('错误信息:', event.message);
console.error('错误行号:', event.lineno);
console.error('错误列号:', event.colno);
console.error('错误文件:', event.filename);
});
</script>
</body>
</html>
