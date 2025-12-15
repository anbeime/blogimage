<[[智能剧本创作与分镜规划平台]]!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>智能PPT生成工具 - 快速创建专业演示文稿</title>
    <!-- Tailwind CSS v3 -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.8/dist/chart.umd.min.js"></script>
    <!-- 统一的 Tailwind 配置 -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#1E40AF', // 商务蓝
                        secondary: '#F97316', // 橙色强调色
                        neutral: {
                            100: '#F3F4F6',
                            200: '#E5E7EB',
                            300: '#D1D5DB',
                            400: '#9CA3AF',
                            500: '#6B7280',
                            600: '#4B5563',
                            700: '#374151',
                            800: '#1F2937',
                            900: '#111827',
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                    },
                    boxShadow: {
                        'card': '0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)',
                        'card-hover': '0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05)',
                    },
                    animation: {
                        'fade-in': 'fadeIn 0.5s ease-in-out',
                        'slide-in': 'slideIn 0.5s ease-in-out',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                    },
                    keyframes: {
                        fadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        slideIn: {
                            '0%': { transform: 'translateY(20px)', opacity: '0' },
                            '100%': { transform: 'translateY(0)', opacity: '1' },
                        }
                    }
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .glass-effect {
                @apply bg-white bg-opacity-20 backdrop-blur-lg;
            }
            .text-gradient {
                @apply bg-clip-text text-transparent bg-gradient-to-r from-primary to-blue-400;
            }
            .btn-primary {
                @apply bg-primary hover:bg-blue-800 text-white font-medium py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50;
            }
            .btn-secondary {
                @apply bg-secondary hover:bg-orange-600 text-white font-medium py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-orange-500 focus:ring-opacity-50;
            }
            .btn-outline {
                @apply border border-primary text-primary hover:bg-primary hover:text-white font-medium py-2 px-4 rounded-lg transition-all duration-300 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50;
            }
            .card {
                @apply bg-white rounded-xl shadow-card p-6 transition-all duration-300 hover:shadow-card-hover;
            }
            .input-field {
                @apply w-full px-4 py-2 border border-neutral-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent transition-all duration-300;
            }
            .nav-link {
                @apply flex items-center gap-2 px-4 py-3 rounded-lg transition-all duration-300;
            }
            .nav-link.active {
                @apply bg-primary text-white;
            }
            .nav-link:not(.active) {
                @apply text-neutral-600 hover:bg-neutral-100;
            }
            .template-card {
                @apply relative overflow-hidden rounded-xl shadow-card transition-all duration-300 hover:shadow-card-hover cursor-pointer;
            }
            .template-card:hover .template-overlay {
                @apply opacity-100;
            }
            .template-overlay {
                @apply absolute inset-0 bg-primary bg-opacity-70 flex items-center justify-center opacity-0 transition-opacity duration-300;
            }
            .skeleton {
                @apply animate-pulse bg-neutral-200 rounded;
            }
        }
    </style>
</head>
<body class="bg-neutral-100 font-sans text-neutral-800 min-h-screen">
    <!-- 顶部导航栏 -->
    <header class="bg-white shadow-sm sticky top-0 z-50">
        <div class="container mx-auto px-4 py-3 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <div class="text-primary text-2xl">
                    <i class="fa fa-file-powerpoint-o"></i>
                </div>
                <h1 class="text-xl font-bold text-primary">智能PPT生成器</h1>
            </div>
            <nav class="hidden md:flex items-center gap-6">
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors">首页</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors">功能介绍</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors">使用教程</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors">常见问题</a>
            </nav>
            <div class="flex items-center gap-3">
                <button class="btn-outline hidden md:block">登录</button>
                <button class="btn-primary">免费试用</button>
                <button class="md:hidden text-neutral-600" id="mobile-menu-button">
                    <i class="fa fa-bars text-xl"></i>
                </button>
            </div>
        </div>
        <!-- 移动端菜单 -->
        <div id="mobile-menu" class="md:hidden hidden bg-white border-t border-neutral-200 animate-fade-in">
            <div class="container mx-auto px-4 py-3 flex flex-col gap-3">
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors py-2">首页</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors py-2">功能介绍</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors py-2">使用教程</a>
                <a href="#" class="text-neutral-600 hover:text-primary transition-colors py-2">常见问题</a>
                <button class="btn-outline w-full">登录</button>
            </div>
        </div>
    </header>

    <!-- 主内容区 -->
    <main class="container mx-auto px-4 py-6 flex flex-col lg:flex-row gap-6">
        <!-- 左侧功能导航 -->
        <aside class="lg:w-64 bg-white rounded-xl shadow-sm p-4 h-fit sticky top-20">
            <nav class="flex flex-col gap-2">
                <button class="nav-link active" data-section="theme-generation">
                    <i class="fa fa-lightbulb-o w-5 text-center"></i>
                    <span>主题生成</span>
                </button>
                <button class="nav-link" data-section="template-recommendation">
                    <i class="fa fa-th-large w-5 text-center"></i>
                    <span>模板推荐</span>
                </button>
                <button class="nav-link" data-section="content-filling">
                    <i class="fa fa-pencil-square-o w-5 text-center"></i>
                    <span>内容填充</span>
                </button>
                <button class="nav-link" data-section="ai-image">
                    <i class="fa fa-picture-o w-5 text-center"></i>
                    <span>AI智能配图</span>
                </button>
            </nav>
            <div class="mt-8 p-4 bg-blue-50 rounded-lg">
                <h3 class="font-medium text-primary mb-2">使用提示</h3>
                <p class="text-sm text-neutral-600">输入清晰的主题或大纲，获得更精准的PPT内容建议。</p>
            </div>
        </aside>

        <!-- 右侧主内容 -->
        <section class="flex-1">
            <!-- 主题生成模块 -->
            <div id="theme-generation" class="section-content animate-fade-in">
                <div class="card mb-6">
                    <h2 class="text-2xl font-bold mb-4">主题生成</h2>
                    <p class="text-neutral-600 mb-6">输入您的PPT主题，我们将为您生成专业的演示大纲</p>
                    <form id="theme-form" class="space-y-4">
                        <div>
                            <label for="theme-input" class="block text-sm font-medium text-neutral-700 mb-1">输入主题</label>
                            <input type="text" id="theme-input" class="input-field" placeholder="例如：2023年销售工作总结" required>
                        </div>
                        <div>
                            <label for="theme-type" class="block text-sm font-medium text-neutral-700 mb-1">演示类型</label>
                            <select id="theme-type" class="input-field">
                                <option value="business">商务汇报</option>
                                <option value="education">教育培训</option>
                                <option value="marketing">市场营销</option>
                                <option value="project">项目展示</option>
                                <option value="other">其他类型</option>
                            </select>
                        </div>
                        <div>
                            <label for="slide-count" class="block text-sm font-medium text-neutral-700 mb-1">建议页数</label>
                            <input type="range" id="slide-count" min="5" max="30" value="15" class="w-full h-2 bg-neutral-200 rounded-lg appearance-none cursor-pointer">
                            <div class="flex justify-between text-xs text-neutral-500 mt-1">
                                <span>5页</span>
                                <span id="slide-count-value">15页</span>
                                <span>30页</span>
                            </div>
                        </div>
                        <button type="submit" class="btn-primary w-full">
                            <i class="fa fa-magic mr-2"></i>生成大纲
                        </button>
                    </form>
                </div>

                <!-- 生成结果预览 -->
                <div id="theme-result" class="hidden">
                    <div class="card mb-6">
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-xl font-bold">生成的大纲</h3>
                            <div class="flex gap-2">
                                <button class="btn-outline py-1 px-3 text-sm" id="edit-outline">
                                    <i class="fa fa-pencil mr-1"></i>编辑
                                </button>
                                <button class="btn-primary py-1 px-3 text-sm" id="save-outline">
                                    <i class="fa fa-save mr-1"></i>保存
                                </button>
                            </div>
                        </div>
                        <div id="outline-content" class="space-y-3">
                            <!-- 生成的大纲内容将在这里显示 -->
                        </div>
                    </div>

                    <div class="flex justify-between">
                        <button class="btn-outline" id="regenerate-outline">
                            <i class="fa fa-refresh mr-2"></i>重新生成
                        </button>
                        <button class="btn-secondary" id="go-to-templates">
                            选择模板 <i class="fa fa-arrow-right ml-2"></i>
                        </button>
                    </div>
                </div>
            </div>

            <!-- 模板推荐模块 -->
            <div id="template-recommendation" class="section-content hidden animate-fade-in">
                <div class="card mb-6">
                    <h2 class="text-2xl font-bold mb-4">模板推荐</h2>
                    <p class="text-neutral-600 mb-6">根据您的需求，我们为您推荐以下PPT模板</p>
                    
                    <!-- 模板筛选 -->
                    <div class="flex flex-wrap gap-3 mb-6">
                        <button class="px-4 py-2 rounded-full bg-primary text-white text-sm">全部</button>
                        <button class="px-4 py-2 rounded-full bg-white border border-neutral-300 text-neutral-600 text-sm hover:bg-neutral-50">商务风格</button>
                        <button class="px-4 py-2 rounded-full bg-white border border-neutral-300 text-neutral-600 text-sm hover:bg-neutral-50">创意设计</button>
                        <button class="px-4 py-2 rounded-full bg-white border border-neutral-300 text-neutral-600 text-sm hover:bg-neutral-50">简约风格</button>
                        <button class="px-4 py-2 rounded-full bg-white border border-neutral-300 text-neutral-600 text-sm hover:bg-neutral-50">科技风格</button>
                        <button class="px-4 py-2 rounded-full bg-white border border-neutral-300 text-neutral-600 text-sm hover:bg-neutral-50">教育风格</button>
                    </div>

                    <!-- 模板网格 -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                        <!-- 模板1 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/2255495444158873612~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=XRHP9EwbiUlgP8JRR%2BAhWPsuUU8%3D" alt="商务PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">专业商务模板</h3>
                                <p class="text-sm text-neutral-500">20页 | 适合商务汇报</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                        
                        <!-- 模板2 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/labis/863fb90599a44323b54c4d7cb630335a~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=KCkOqnIHq7jI7zAW8DKAttBMJhg%3D" alt="创意PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">创意设计模板</h3>
                                <p class="text-sm text-neutral-500">15页 | 适合营销展示</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                        
                        <!-- 模板3 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/labis/7233bec5ba535034a884ed7006706aec~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=J3FUclp2iaoK4yeTZ%2Fqy5KlR3S4%3D" alt="简约PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">简约风格模板</h3>
                                <p class="text-sm text-neutral-500">12页 | 适合教育培训</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                        
                        <!-- 模板4 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/ecom-shop-material/jpeg_m_1416b31871a76a58b3205875574afa7f_sx_3351619_www5000-5000~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=5Fzvo59JzdY4PFrHVPw%2B2wfpCc8%3D" alt="科技PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">科技风格模板</h3>
                                <p class="text-sm text-neutral-500">25页 | 适合项目展示</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                        
                        <!-- 模板5 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/ecom-shop-material/jpeg_m_fab7a6bb68dc7b11a19ee2d247456a73_sx_117167_www750-750~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=Zz8k5Wi3HQO47u6PHJ0yP8s5LYM%3D" alt="年终总结PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">年终总结模板</h3>
                                <p class="text-sm text-neutral-500">18页 | 适合工作总结</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                        
                        <!-- 模板6 -->
                        <div class="template-card">
                            <img src="https://p11-doubao-search-sign.byteimg.com/labis/8f8ec8dbf8b4513ba2c660e9a197793a~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=lWj9i1HHNucrpG%2BGg%2B5mDHrIFeQ%3D" alt="创意PPT模板" class="w-full h-48 object-cover">
                            <div class="p-3 bg-white">
                                <h3 class="font-medium">创意花艺模板</h3>
                                <p class="text-sm text-neutral-500">10页 | 适合创意展示</p>
                            </div>
                            <div class="template-overlay">
                                <button class="btn-primary">选择此模板</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 内容填充模块 -->
            <div id="content-filling" class="section-content hidden animate-fade-in">
                <div class="card mb-6">
                    <h2 class="text-2xl font-bold mb-4">内容填充</h2>
                    <p class="text-neutral-600 mb-6">提供您的PPT大纲或详细要求，我们将为您生成完整的PPT内容</p>
                    
                    <div class="mb-6">
                        <h3 class="font-medium mb-3">选择输入方式</h3>
                        <div class="flex flex-wrap gap-3">
                            <button class="px-4 py-2 rounded-lg bg-primary text-white text-sm flex items-center gap-2">
                                <i class="fa fa-list"></i>
                                <span>导入大纲</span>
                            </button>
                            <button class="px-4 py-2 rounded-lg bg-white border border-neutral-300 text-neutral-600 text-sm flex items-center gap-2 hover:bg-neutral-50">
                                <i class="fa fa-upload"></i>
                                <span>上传文件</span>
                            </button>
                            <button class="px-4 py-2 rounded-lg bg-white border border-neutral-300 text-neutral-600 text-sm flex items-center gap-2 hover:bg-neutral-50">
                                <i class="fa fa-magic"></i>
                                <span>使用AI生成</span>
                            </button>
                        </div>
                    </div>
                    
                    <form id="content-form" class="space-y-4">
                        <div>
                            <label for="content-outline" class="block text-sm font-medium text-neutral-700 mb-1">PPT大纲</label>
                            <textarea id="content-outline" rows="8" class="input-field" placeholder="请输入您的PPT大纲，每行一个标题。例如：
1. 公司简介
2. 产品介绍
3. 市场分析
4. 竞争优势
5. 发展规划
6. 联系方式"></textarea>
                        </div>
                        
                        <div>
                            <label for="content-detail" class="block text-sm font-medium text-neutral-700 mb-1">详细要求（可选）</label>
                            <textarea id="content-detail" rows="4" class="input-field" placeholder="请描述您对PPT内容的具体要求，如风格、重点内容、数据展示方式等..."></textarea>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-neutral-700 mb-1">内容选项</label>
                            <div class="space-y-2">
                                <div class="flex items-center">
                                    <input type="checkbox" id="include-title" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300 rounded" checked>
                                    <label for="include-title" class="ml-2 text-sm text-neutral-700">包含标题页</label>
                                </div>
                                <div class="flex items-center">
                                    <input type="checkbox" id="include-agenda" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300 rounded" checked>
                                    <label for="include-agenda" class="ml-2 text-sm text-neutral-700">包含目录页</label>
                                </div>
                                <div class="flex items-center">
                                    <input type="checkbox" id="include-summary" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300 rounded" checked>
                                    <label for="include-summary" class="ml-2 text-sm text-neutral-700">包含总结页</label>
                                </div>
                                <div class="flex items-center">
                                    <input type="checkbox" id="include-qna" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300 rounded">
                                    <label for="include-qna" class="ml-2 text-sm text-neutral-700">包含问答页</label>
                                </div>
                            </div>
                        </div>
                        
                        <button type="submit" class="btn-primary w-full">
                            <i class="fa fa-file-text-o mr-2"></i>生成PPT内容
                        </button>
                    </form>
                </div>
                
                <!-- 内容预览 -->
                <div id="content-preview" class="hidden">
                    <div class="card mb-6">
                        <div class="flex justify-between items-center mb-4">
                            <h3 class="text-xl font-bold">PPT内容预览</h3>
                            <div class="flex gap-2">
                                <button class="btn-outline py-1 px-3 text-sm">
                                    <i class="fa fa-download mr-1"></i>下载
                                </button>
                                <button class="btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-share-alt mr-1"></i>分享
                                </button>
                            </div>
                        </div>
                        
                        <div class="bg-neutral-100 rounded-lg p-4 mb-4">
                            <div class="flex items-center justify-between mb-2">
                                <h4 class="font-medium">第1页：标题页</h4>
                                <div class="text-xs text-neutral-500">1/6</div>
                            </div>
                            <div class="bg-white rounded shadow-sm p-4 min-h-[200px] flex flex-col items-center justify-center">
                                <h1 class="text-2xl font-bold text-center mb-2">公司产品发布会</h1>
                                <p class="text-neutral-500 text-center">2023年12月15日</p>
                                <div class="mt-6 w-16 h-16 bg-primary rounded-full flex items-center justify-center text-white">
                                    <i class="fa fa-rocket text-2xl"></i>
                                </div>
                            </div>
                        </div>
                        
                        <div class="bg-neutral-100 rounded-lg p-4 mb-4">
                            <div class="flex items-center justify-between mb-2">
                                <h4 class="font-medium">第2页：目录页</h4>
                                <div class="text-xs text-neutral-500">2/6</div>
                            </div>
                            <div class="bg-white rounded shadow-sm p-4 min-h-[200px]">
                                <h2 class="text-xl font-bold mb-4 text-center">目录</h2>
                                <ul class="space-y-2">
                                    <li class="flex items-center">
                                        <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3">1</span>
                                        <span>公司简介</span>
                                    </li>
                                    <li class="flex items-center">
                                        <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3">2</span>
                                        <span>产品介绍</span>
                                    </li>
                                    <li class="flex items-center">
                                        <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3">3</span>
                                        <span>市场分析</span>
                                    </li>
                                    <li class="flex items-center">
                                        <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3">4</span>
                                        <span>竞争优势</span>
                                    </li>
                                    <li class="flex items-center">
                                        <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3">5</span>
                                        <span>发展规划</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        
                        <div class="flex justify-center gap-4 mt-6">
                            <button class="btn-outline py-1 px-4">
                                <i class="fa fa-arrow-left mr-2"></i>上一页
                            </button>
                            <button class="btn-primary py-1 px-4">
                                下一页<i class="fa fa-arrow-right ml-2"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- AI智能配图模块 -->
            <div id="ai-image" class="section-content hidden animate-fade-in">
                <div class="card mb-6">
                    <h2 class="text-2xl font-bold mb-4">AI智能配图</h2>
                    <p class="text-neutral-600 mb-6">根据您的PPT内容，我们将为您推荐合适的图片素材</p>
                    
                    <form id="image-form" class="space-y-4">
                        <div>
                            <label for="image-topic" class="block text-sm font-medium text-neutral-700 mb-1">图片主题</label>
                            <input type="text" id="image-topic" class="input-field" placeholder="例如：商务会议、科技创新、团队合作" required>
                        </div>
                        
                        <div>
                            <label for="image-style" class="block text-sm font-medium text-neutral-700 mb-1">图片风格</label>
                            <select id="image-style" class="input-field">
                                <option value="business">商务风格</option>
                                <option value="creative">创意设计</option>
                                <option value="minimal">简约风格</option>
                                <option value="technology">科技风格</option>
                                <option value="nature">自然风景</option>
                                <option value="abstract">抽象图形</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-neutral-700 mb-1">图片数量</label>
                            <div class="flex items-center gap-4">
                                <label class="inline-flex items-center">
                                    <input type="radio" name="image-count" value="4" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300" checked>
                                    <span class="ml-2 text-sm text-neutral-700">4张</span>
                                </label>
                                <label class="inline-flex items-center">
                                    <input type="radio" name="image-count" value="8" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300">
                                    <span class="ml-2 text-sm text-neutral-700">8张</span>
                                </label>
                                <label class="inline-flex items-center">
                                    <input type="radio" name="image-count" value="12" class="w-4 h-4 text-primary focus:ring-primary border-neutral-300">
                                    <span class="ml-2 text-sm text-neutral-700">12张</span>
                                </label>
                            </div>
                        </div>
                        
                        <button type="submit" class="btn-primary w-full">
                            <i class="fa fa-search mr-2"></i>搜索图片
                        </button>
                    </form>
                </div>
                
                <!-- 图片搜索结果 -->
                <div id="image-results" class="hidden">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-xl font-bold">推荐图片</h3>
                        <div class="flex gap-2">
                            <button class="btn-outline py-1 px-3 text-sm">
                                <i class="fa fa-download mr-1"></i>批量下载
                            </button>
                            <button class="btn-primary py-1 px-3 text-sm">
                                <i class="fa fa-plus mr-1"></i>添加到PPT
                            </button>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4 gap-4">
                        <!-- 图片1 -->
                        <div class="relative group">
                            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/dab44aa9024e42d6ad859c1dda4aa772~tplv-a9rns2rl98-image.image?rcl=20251208112212F3BF74FE43E9318EB1F6&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1767756170&x-signature=QIoO3iaWl4gSDfEfOO43hbSe2mI%3D" alt="商务会议" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片2 -->
                        <div class="relative group">
                            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/303742185455460e8a9f4b7ba0e426c0~tplv-a9rns2rl98-image.image?rcl=20251208112212F3BF74FE43E9318EB1F6&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1767756175&x-signature=%2Fzqri1Z%2FySsgQDg3Gx2pdmeCmII%3D" alt="数据分析" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片3 -->
                        <div class="relative group">
                            <img src="https://p9-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/8690fe91b5a448a285a544a80e4ff765~tplv-a9rns2rl98-image.image?rcl=20251208112212F3BF74FE43E9318EB1F6&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1767756174&x-signature=9H6HSZ6AtNzicX9gW1R81EFotGs%3D" alt="团队合作" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片4 -->
                        <div class="relative group">
                            <img src="https://p11-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/2309090966592290842~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=l8%2BakmSmVmBY2MkwNwCvf69mm3Y%3D" alt="创意图表" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片5 -->
                        <div class="relative group">
                            <img src="https://p11-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/936162889004613649~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=fDkU4ZfLmHjkV6HPJ4ztQqQRo6o%3D" alt="创意图标" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片6 -->
                        <div class="relative group">
                            <img src="https://p11-doubao-search-sign.byteimg.com/tos-cn-i-be4g95zd3a/2345379652179460130~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=AjsUQMDBwSsz1aKyfuDGgnAnbYU%3D" alt="流程图" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片7 -->
                        <div class="relative group">
                            <img src="https://p26-doubao-search-sign.byteimg.com/labis/648f01d611f08e856913183e5684e6db~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=iP4CWnVjMfSH%2FbEPXf24TdtjPUU%3D" alt="星形图表" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                        
                        <!-- 图片8 -->
                        <div class="relative group">
                            <img src="https://p26-doubao-search-sign.byteimg.com/labis/badbcb074cccb6a370f3d97645529620~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1780716152&x-signature=PVu9%2B8tYhOcfhzVer5Ni%2BdtxvCU%3D" alt="商务图表" class="w-full h-40 object-cover rounded-lg">
                            <div class="absolute inset-0 bg-primary bg-opacity-0 group-hover:bg-opacity-50 transition-all duration-300 rounded-lg flex items-center justify-center">
                                <button class="opacity-0 group-hover:opacity-100 transition-opacity duration-300 btn-primary py-1 px-3 text-sm">
                                    <i class="fa fa-plus mr-1"></i>选择
                                </button>
                            </div>
                        </div>
                    </div>
                    
                    <div class="mt-6 flex justify-center">
                        <button class="btn-outline">
                            <i class="fa fa-refresh mr-2"></i>加载更多
                        </button>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- 底部信息 -->
    <footer class="bg-white border-t border-neutral-200 mt-12 py-8">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <div class="flex items-center gap-2 mb-4">
                        <div class="text-primary text-2xl">
                            <i class="fa fa-file-powerpoint-o"></i>
                        </div>
                        <h2 class="text-xl font-bold text-primary">智能PPT生成器</h2>
                    </div>
                    <p class="text-neutral-600 text-sm">
                        让PPT制作变得简单高效，帮助您快速创建专业水准的演示文稿。
                    </p>
                    <div class="flex gap-4 mt-4">
                        <a href="#" class="text-neutral-500 hover:text-primary transition-colors">
                            <i class="fa fa-weixin text-xl"></i>
                        </a>
                        <a href="#" class="text-neutral-500 hover:text-primary transition-colors">
                            <i class="fa fa-weibo text-xl"></i>
                        </a>
                        <a href="#" class="text-neutral-500 hover:text-primary transition-colors">
                            <i class="fa fa-qq text-xl"></i>
                        </a>
                    </div>
                </div>
                
                <div>
                    <h3 class="font-bold mb-4">产品功能</h3>
                    <ul class="space-y-2 text-sm text-neutral-600">
                        <li><a href="#" class="hover:text-primary transition-colors">主题生成</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">模板推荐</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">内容填充</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">AI智能配图</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">PPT美化</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="font-bold mb-4">帮助中心</h3>
                    <ul class="space-y-2 text-sm text-neutral-600">
                        <li><a href="#" class="hover:text-primary transition-colors">使用教程</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">常见问题</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">功能介绍</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">意见反馈</a></li>
                        <li><a href="#" class="hover:text-primary transition-colors">联系我们</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="font-bold mb-4">联系我们</h3>
                    <ul class="space-y-2 text-sm text-neutral-600">
                        <li class="flex items-center gap-2">
                            <i class="fa fa-envelope-o text-primary"></i>
                            <span>support@smartppt.com</span>
                        </li>
                        <li class="flex items-center gap-2">
                            <i class="fa fa-phone text-primary"></i>
                            <span>400-123-4567</span>
                        </li>
                        <li class="flex items-center gap-2">
                            <i class="fa fa-map-marker text-primary"></i>
                            <span>北京市海淀区中关村</span>
                        </li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-neutral-200 mt-8 pt-6 text-center text-sm text-neutral-500">
                <p>© 2023 智能PPT生成器 版权所有</p>
            </div>
        </div>
    </footer>

    <!-- JavaScript -->
    <script>
        // 移动端菜单切换
        document.getElementById('mobile-menu-button').addEventListener('click', function() {
            const mobileMenu = document.getElementById('mobile-menu');
            mobileMenu.classList.toggle('hidden');
        });

        // 导航切换
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function() {
                // 移除所有活动状态
                document.querySelectorAll('.nav-link').forEach(item => {
                    item.classList.remove('active');
                });
                
                // 添加活动状态
                this.classList.add('active');
                
                // 隐藏所有内容
                document.querySelectorAll('.section-content').forEach(content => {
                    content.classList.add('hidden');
                });
                
                // 显示对应内容
                const sectionId = this.getAttribute('data-section');
                document.getElementById(sectionId).classList.remove('hidden');
            });
        });

        // 页数滑块
        const slideCount = document.getElementById('slide-count');
        const slideCountValue = document.getElementById('slide-count-value');
        
        slideCount.addEventListener('input', function() {
            slideCountValue.textContent = this.value + '页';
        });

        // 主题生成表单提交
        document.getElementById('theme-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const themeInput = document.getElementById('theme-input').value;
            const themeType = document.getElementById('theme-type').value;
            const slideCount = document.getElementById('slide-count').value;
            
            // 显示加载状态
            this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-spinner fa-spin mr-2"></i>生成中...';
            
            // 模拟API请求延迟
            setTimeout(() => {
                // 生成大纲内容
                const outlineContent = document.getElementById('outline-content');
                outlineContent.innerHTML = generateOutline(themeInput, themeType, slideCount);
                
                // 显示结果
                document.getElementById('theme-result').classList.remove('hidden');
                
                // 恢复按钮状态
                this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-magic mr-2"></i>生成大纲';
                
                // 滚动到结果区域
                document.getElementById('theme-result').scrollIntoView({ behavior: 'smooth' });
            }, 1500);
        });

        // 生成大纲内容
        function generateOutline(theme, type, count) {
            // 根据不同类型生成不同大纲
            let outline = '';
            
            if (type === 'business') {
                outline = `
                    <div class="p-3 bg-blue-50 rounded-lg">
                        <h3 class="font-bold text-lg mb-2">${theme}</h3>
                        <p class="text-sm text-neutral-600 mb-2">专业商务演示大纲</p>
                        <div class="flex items-center gap-2 text-sm text-neutral-500">
                            <span><i class="fa fa-file-text-o mr-1"></i>${count}页</span>
                            <span><i class="fa fa-clock-o mr-1"></i>建议演示时间: ${Math.ceil(count/2)}分钟</span>
                        </div>
                    </div>
                    <div class="mt-4 space-y-2">
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">1</span>
                            <div>
                                <h4 class="font-medium">封面页</h4>
                                <p class="text-sm text-neutral-500">${theme}</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">2</span>
                            <div>
                                <h4 class="font-medium">目录</h4>
                                <p class="text-sm text-neutral-500">概述演示内容和结构</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">3</span>
                            <div>
                                <h4 class="font-medium">背景介绍</h4>
                                <p class="text-sm text-neutral-500">相关背景信息和重要性</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">4</span>
                            <div>
                                <h4 class="font-medium">目标与愿景</h4>
                                <p class="text-sm text-neutral-500">设定明确的目标和预期成果</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">5</span>
                            <div>
                                <h4 class="font-medium">数据分析</h4>
                                <p class="text-sm text-neutral-500">关键数据和趋势图表</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">6</span>
                            <div>
                                <h4 class="font-medium">实施方案</h4>
                                <p class="text-sm text-neutral-500">具体行动计划和步骤</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">7</span>
                            <div>
                                <h4 class="font-medium">资源需求</h4>
                                <p class="text-sm text-neutral-500">所需人力、物力和财力资源</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">8</span>
                            <div>
                                <h4 class="font-medium">时间规划</h4>
                                <p class="text-sm text-neutral-500">项目时间线和关键节点</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">9</span>
                            <div>
                                <h4 class="font-medium">风险评估</h4>
                                <p class="text-sm text-neutral-500">潜在风险和应对措施</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">10</span>
                            <div>
                                <h4 class="font-medium">总结与展望</h4>
                                <p class="text-sm text-neutral-500">主要结论和未来展望</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">11</span>
                            <div>
                                <h4 class="font-medium">问答环节</h4>
                                <p class="text-sm text-neutral-500">准备回答问题</p>
                            </div>
                        </div>
                    </div>
                `;
            } else if (type === 'education') {
                outline = `
                    <div class="p-3 bg-blue-50 rounded-lg">
                        <h3 class="font-bold text-lg mb-2">${theme}</h3>
                        <p class="text-sm text-neutral-600 mb-2">教育培训演示大纲</p>
                        <div class="flex items-center gap-2 text-sm text-neutral-500">
                            <span><i class="fa fa-file-text-o mr-1"></i>${count}页</span>
                            <span><i class="fa fa-clock-o mr-1"></i>建议授课时间: ${Math.ceil(count/1.5)}分钟</span>
                        </div>
                    </div>
                    <div class="mt-4 space-y-2">
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">1</span>
                            <div>
                                <h4 class="font-medium">封面页</h4>
                                <p class="text-sm text-neutral-500">${theme}</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">2</span>
                            <div>
                                <h4 class="font-medium">课程介绍</h4>
                                <p class="text-sm text-neutral-500">课程目标和学习成果</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">3</span>
                            <div>
                                <h4 class="font-medium">知识回顾</h4>
                                <p class="text-sm text-neutral-500">相关基础知识复习</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">4</span>
                            <div>
                                <h4 class="font-medium">核心概念</h4>
                                <p class="text-sm text-neutral-500">关键术语和定义</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">5</span>
                            <div>
                                <h4 class="font-medium">原理讲解</h4>
                                <p class="text-sm text-neutral-500">理论基础和工作原理</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">6</span>
                            <div>
                                <h4 class="font-medium">实例分析</h4>
                                <p class="text-sm text-neutral-500">实际案例讲解</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">7</span>
                            <div>
                                <h4 class="font-medium">实践演示</h4>
                                <p class="text-sm text-neutral-500">操作步骤和技巧</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">8</span>
                            <div>
                                <h4 class="font-medium">常见问题</h4>
                                <p class="text-sm text-neutral-500">典型错误和解决方案</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">9</span>
                            <div>
                                <h4 class="font-medium">拓展思考</h4>
                                <p class="text-sm text-neutral-500">深入探讨和应用场景</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">10</span>
                            <div>
                                <h4 class="font-medium">总结归纳</h4>
                                <p class="text-sm text-neutral-500">重点内容回顾</p>
                            </div>
                        </div>
                    </div>
                `;
            } else if (type === 'marketing') {
                outline = `
                    <div class="p-3 bg-blue-50 rounded-lg">
                        <h3 class="font-bold text-lg mb-2">${theme}</h3>
                        <p class="text-sm text-neutral-600 mb-2">市场营销演示大纲</p>
                        <div class="flex items-center gap-2 text-sm text-neutral-500">
                            <span><i class="fa fa-file-text-o mr-1"></i>${count}页</span>
                            <span><i class="fa fa-clock-o mr-1"></i>建议演示时间: ${Math.ceil(count/2)}分钟</span>
                        </div>
                    </div>
                    <div class="mt-4 space-y-2">
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">1</span>
                            <div>
                                <h4 class="font-medium">封面页</h4>
                                <p class="text-sm text-neutral-500">${theme}</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">2</span>
                            <div>
                                <h4 class="font-medium">市场概述</h4>
                                <p class="text-sm text-neutral-500">行业现状和发展趋势</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">3</span>
                            <div>
                                <h4 class="font-medium">目标受众</h4>
                                <p class="text-sm text-neutral-500">用户画像和需求分析</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">4</span>
                            <div>
                                <h4 class="font-medium">竞争分析</h4>
                                <p class="text-sm text-neutral-500">主要竞争对手研究</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">5</span>
                            <div>
                                <h4 class="font-medium">产品优势</h4>
                                <p class="text-sm text-neutral-500">核心卖点和差异化</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">6</span>
                            <div>
                                <h4 class="font-medium">营销策略</h4>
                                <p class="text-sm text-neutral-500">推广渠道和方法</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">7</span>
                            <div>
                                <h4 class="font-medium">内容计划</h4>
                                <p class="text-sm text-neutral-500">内容创作和发布策略</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">8</span>
                            <div>
                                <h4 class="font-medium">预算分配</h4>
                                <p class="text-sm text-neutral-500">营销预算和ROI预测</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">9</span>
                            <div>
                                <h4 class="font-medium">时间安排</h4>
                                <p class="text-sm text-neutral-500">营销活动时间表</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">10</span>
                            <div>
                                <h4 class="font-medium">效果评估</h4>
                                <p class="text-sm text-neutral-500">KPI设定和监控方法</p>
                            </div>
                        </div>
                    </div>
                `;
            } else if (type === 'project') {
                outline = `
                    <div class="p-3 bg-blue-50 rounded-lg">
                        <h3 class="font-bold text-lg mb-2">${theme}</h3>
                        <p class="text-sm text-neutral-600 mb-2">项目展示演示大纲</p>
                        <div class="flex items-center gap-2 text-sm text-neutral-500">
                            <span><i class="fa fa-file-text-o mr-1"></i>${count}页</span>
                            <span><i class="fa fa-clock-o mr-1"></i>建议演示时间: ${Math.ceil(count/2)}分钟</span>
                        </div>
                    </div>
                    <div class="mt-4 space-y-2">
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">1</span>
                            <div>
                                <h4 class="font-medium">封面页</h4>
                                <p class="text-sm text-neutral-500">${theme}</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">2</span>
                            <div>
                                <h4 class="font-medium">项目概述</h4>
                                <p class="text-sm text-neutral-500">项目背景和目标</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">3</span>
                            <div>
                                <h4 class="font-medium">团队介绍</h4>
                                <p class="text-sm text-neutral-500">核心成员和职责</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">4</span>
                            <div>
                                <h4 class="font-medium">需求分析</h4>
                                <p class="text-sm text-neutral-500">用户需求和痛点</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">5</span>
                            <div>
                                <h4 class="font-medium">解决方案</h4>
                                <p class="text-sm text-neutral-500">产品功能和特点</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">6</span>
                            <div>
                                <h4 class="font-medium">技术架构</h4>
                                <p class="text-sm text-neutral-500">系统设计和技术选型</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">7</span>
                            <div>
                                <h4 class="font-medium">开发流程</h4>
                                <p class="text-sm text-neutral-500">项目阶段和方法论</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">8</span>
                            <div>
                                <h4 class="font-medium">成果展示</h4>
                                <p class="text-sm text-neutral-500">产品演示和案例</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">9</span>
                            <div>
                                <h4 class="font-medium">挑战与解决</h4>
                                <p class="text-sm text-neutral-500">项目难点和应对措施</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">10</span>
                            <div>
                                <h4 class="font-medium">未来规划</h4>
                                <p class="text-sm text-neutral-500">后续迭代和发展方向</p>
                            </div>
                        </div>
                    </div>
                `;
            } else {
                outline = `
                    <div class="p-3 bg-blue-50 rounded-lg">
                        <h3 class="font-bold text-lg mb-2">${theme}</h3>
                        <p class="text-sm text-neutral-600 mb-2">通用演示大纲</p>
                        <div class="flex items-center gap-2 text-sm text-neutral-500">
                            <span><i class="fa fa-file-text-o mr-1"></i>${count}页</span>
                            <span><i class="fa fa-clock-o mr-1"></i>建议演示时间: ${Math.ceil(count/2)}分钟</span>
                        </div>
                    </div>
                    <div class="mt-4 space-y-2">
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">1</span>
                            <div>
                                <h4 class="font-medium">封面页</h4>
                                <p class="text-sm text-neutral-500">${theme}</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">2</span>
                            <div>
                                <h4 class="font-medium">概述</h4>
                                <p class="text-sm text-neutral-500">主题简介和重要性</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">3</span>
                            <div>
                                <h4 class="font-medium">背景信息</h4>
                                <p class="text-sm text-neutral-500">相关背景和上下文</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">4</span>
                            <div>
                                <h4 class="font-medium">核心内容一</h4>
                                <p class="text-sm text-neutral-500">主要观点和论据</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">5</span>
                            <div>
                                <h4 class="font-medium">核心内容二</h4>
                                <p class="text-sm text-neutral-500">主要观点和论据</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">6</span>
                            <div>
                                <h4 class="font-medium">核心内容三</h4>
                                <p class="text-sm text-neutral-500">主要观点和论据</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">7</span>
                            <div>
                                <h4 class="font-medium">案例分析</h4>
                                <p class="text-sm text-neutral-500">实际例子和应用</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">8</span>
                            <div>
                                <h4 class="font-medium">总结</h4>
                                <p class="text-sm text-neutral-500">主要结论和要点</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">9</span>
                            <div>
                                <h4 class="font-medium">展望</h4>
                                <p class="text-sm text-neutral-500">未来发展和建议</p>
                            </div>
                        </div>
                        <div class="flex items-start">
                            <span class="w-6 h-6 rounded-full bg-primary text-white flex items-center justify-center text-sm mr-3 mt-0.5">10</span>
                            <div>
                                <h4 class="font-medium">问答环节</h4>
                                <p class="text-sm text-neutral-500">准备回答问题</p>
                            </div>
                        </div>
                    </div>
                `;
            }
            
            return outline;
        }

        // 重新生成大纲
        document.getElementById('regenerate-outline').addEventListener('click', function() {
            document.getElementById('theme-result').classList.add('hidden');
            document.getElementById('theme-form').scrollIntoView({ behavior: 'smooth' });
        });

        // 跳转到模板选择
        document.getElementById('go-to-templates').addEventListener('click', function() {
            // 触发模板推荐导航点击
            document.querySelector('[data-section="template-recommendation"]').click();
        });

        // 内容填充表单提交
        document.getElementById('content-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // 显示加载状态
            this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-spinner fa-spin mr-2"></i>生成中...';
            
            // 模拟API请求延迟
            setTimeout(() => {
                // 显示结果
                document.getElementById('content-preview').classList.remove('hidden');
                
                // 恢复按钮状态
                this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-file-text-o mr-2"></i>生成PPT内容';
                
                // 滚动到结果区域
                document.getElementById('content-preview').scrollIntoView({ behavior: 'smooth' });
            }, 1500);
        });

        // 图片搜索表单提交
        document.getElementById('image-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // 显示加载状态
            this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-spinner fa-spin mr-2"></i>搜索中...';
            
            // 模拟API请求延迟
            setTimeout(() => {
                // 显示结果
                document.getElementById('image-results').classList.remove('hidden');
                
                // 恢复按钮状态
                this.querySelector('button[type="submit"]').innerHTML = '<i class="fa fa-search mr-2"></i>搜索图片';
                
                // 滚动到结果区域
                document.getElementById('image-results').scrollIntoView({ behavior: 'smooth' });
            }, 1500);
        });

        // 模板选择
        document.querySelectorAll('.template-card button').forEach(button => {
            button.addEventListener('click', function() {
                // 显示选中效果
                document.querySelectorAll('.template-card button').forEach(btn => {
                    btn.innerHTML = '选择此模板';
                    btn.classList.remove('bg-secondary');
                    btn.classList.add('bg-primary');
                });
                
                this.innerHTML = '<i class="fa fa-check mr-1"></i>已选择';
                this.classList.remove('bg-primary');
                this.classList.add('bg-secondary');
                
                // 显示提示
                const toast = document.createElement('div');
                toast.className = 'fixed bottom-4 right-4 bg-green-500 text-white px-4 py-2 rounded-lg shadow-lg animate-fade-in';
                toast.innerHTML = '<i class="fa fa-check-circle mr-2"></i>模板已选择，正在为您准备内容...';
                document.body.appendChild(toast);
                
                // 3秒后移除提示
                setTimeout(() => {
                    toast.classList.add('animate-fade-out');
                    setTimeout(() => {
                        document.body.removeChild(toast);
                    }, 500);
                }, 3000);
            });
        });

        // 保存大纲
        document.getElementById('save-outline').addEventListener('click', function() {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-4 right-4 bg-green-500 text-white px-4 py-2 rounded-lg shadow-lg animate-fade-in';
            toast.innerHTML = '<i class="fa fa-check-circle mr-2"></i>大纲已保存到您的账户';
            document.body.appendChild(toast);
            
            // 3秒后移除提示
            setTimeout(() => {
                toast.classList.add('animate-fade-out');
                setTimeout(() => {
                    document.body.removeChild(toast);
                }, 500);
            }, 3000);
        });

        // 编辑大纲
        document.getElementById('edit-outline').addEventListener('click', function() {
            alert('编辑功能即将上线，敬请期待！');
        });
    </script>
</body>
</html>