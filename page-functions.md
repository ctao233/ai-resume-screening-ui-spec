# AI简历筛选系统 - 页面功能详细设计

本文档详细描述了AI简历筛选系统各页面的功能设计、交互方式和数据展示规范。

## 1. 登录页面

### 功能组件

1. **登录表单**
   - 用户名/邮箱输入框
   - 密码输入框（带密码显示/隐藏切换）
   - 记住我选项（复选框）
   - 登录按钮（主要按钮）
   - 忘记密码链接

2. **验证码功能**
   - 连续登录失败3次后显示图形验证码
   - 验证码刷新按钮

3. **错误提示**
   - 表单验证错误提示（内联提示）
   - 登录失败错误提示（顶部通知）

### 交互规范

1. **表单验证**
   - 实时验证：输入框失焦时进行格式验证
   - 提交验证：点击登录按钮时进行完整性验证

2. **登录流程**
   - 点击登录按钮后显示加载状态
   - 登录成功后重定向到系统主页
   - 登录失败显示具体错误信息

3. **安全措施**
   - 密码输入错误3次后要求验证码
   - 密码输入错误5次后锁定账户15分钟

## 2. 系统布局

### 功能组件

1. **顶部导航栏**
   - 系统Logo和名称
   - 全局搜索框（支持简历、岗位搜索）
   - 通知中心（带未读消息提示）
   - 用户头像和下拉菜单（个人中心、设置、退出登录）
   - 系统时间显示

2. **侧边菜单**
   - 可折叠设计
   - 一级菜单：仪表盘、简历管理、岗位管理、AI评估、数据分析、系统设置
   - 二级菜单：根据一级菜单展开相应选项
   - 菜单项带有图标和未读/数量提示
   - 当前位置高亮显示

3. **内容区域**
   - 面包屑导航（显示当前位置）
   - 页面标题和操作按钮区
   - 主要内容区域
   - 页脚信息（版权、版本号）

4. **快捷操作悬浮按钮**
   - 上传简历快捷按钮
   - 返回顶部按钮
   - 帮助按钮（显示上下文帮助）

### 交互规范

1. **响应式布局**
   - 桌面端：完整显示侧边栏和顶部导航
   - 平板端：可折叠侧边栏，保留顶部导航
   - 移动端：隐藏侧边栏，使用汉堡菜单，简化顶部导航

2. **菜单交互**
   - 鼠标悬停显示提示文本
   - 点击一级菜单展开/折叠二级菜单
   - 支持键盘导航（Tab键切换，Enter键选择）

3. **主题切换**
   - 支持浅色/深色主题切换
   - 根据系统设置自动切换

## 3. 仪表盘页面

### 功能组件

1. **数据概览卡片**
   - 简历总数（带趋势指标）
   - 岗位总数（带趋势指标）
   - 评估完成数（带趋势指标）
   - 平均匹配度（带趋势指标）

2. **简历处理状态**
   - 环形图显示各状态简历数量占比
   - 状态包括：待处理、处理中、已完成、处理失败
   - 点击可跳转到对应状态的简历列表

3. **热门岗位排行**
   - 显示简历投递量最多的前5个岗位
   - 包含岗位名称、部门、简历数量、环比增长率
   - 点击可跳转到岗位详情

4. **最近活动**
   - 时间轴显示最近的系统活动
   - 活动类型包括：简历上传、岗位创建、评估完成等
   - 显示操作人、操作时间、操作内容
   - 支持筛选特定类型的活动

5. **每日数据趋势图**
   - 折线图显示近30天的数据趋势
   - 数据指标包括：简历上传数、评估完成数
   - 支持时间范围选择（7天、30天、90天）

### 交互规范

1. **数据刷新**
   - 页面加载时自动获取最新数据
   - 提供手动刷新按钮
   - 支持设置自动刷新间隔（关闭、1分钟、5分钟、15分钟）

2. **数据钻取**
   - 点击概览卡片进入对应详情页面
   - 图表支持悬停显示详细数据
   - 支持点击图表元素查看明细数据

3. **个性化设置**
   - 支持拖拽调整卡片位置
   - 支持添加/移除卡片
   - 设置保存到用户偏好

## 4. 简历管理页面

### 功能组件

1. **简历上传区域**
   - 拖拽上传功能
   - 文件选择按钮
   - 批量上传支持
   - 上传进度显示
   - 支持的文件格式提示

2. **简历筛选工具栏**
   - 关键词搜索框（支持候选人姓名、技能、学校等）
   - 高级筛选按钮（弹出筛选面板）
   - 状态筛选下拉菜单
   - 岗位筛选下拉菜单
   - 时间范围选择器
   - 排序选项（上传时间、评分、匹配度）
   - 视图切换（表格视图/卡片视图）

3. **简历列表（表格视图）**
   - 选择列（多选框）
   - 候选人姓名列（带头像）
   - 文件名列（带文件类型图标）
   - 上传时间列
   - 状态列（带状态标签）
   - 评分列（带评分星级显示）
   - 匹配度列（带进度条显示）
   - 操作列（查看、评估、删除按钮）
   - 分页控件

4. **简历列表（卡片视图）**
   - 简历卡片（包含基本信息、状态、评分）
   - 网格布局，响应式调整
   - 卡片悬停效果
   - 快捷操作按钮
   - 无限滚动加载

5. **批量操作工具栏**
   - 批量删除按钮
   - 批量评估按钮
   - 批量导出按钮
   - 批量标记按钮

6. **高级筛选面板**
   - 教育背景筛选（学历、学校、专业）
   - 工作经验筛选（年限、行业、职位）
   - 技能筛选（技能标签多选）
   - 评分范围筛选（滑块控件）
   - 匹配度范围筛选（滑块控件）
   - 自定义标签筛选
   - 重置和应用按钮

### 交互规范

1. **上传交互**
   - 拖拽区域视觉反馈（边框变色、虚线动画）
   - 上传成功/失败提示
   - 文件类型和大小限制提示
   - 上传后自动刷新列表

2. **列表交互**
   - 行悬停高亮
   - 点击行查看详情
   - 双击编辑备注
   - 右键菜单提供快捷操作
   - 列宽可调整
   - 列可自定义显示/隐藏

3. **筛选交互**
   - 筛选条件变更后自动应用（延迟300ms）
   - 筛选条件显示为标签，可快速删除
   - 保存常用筛选条件组合
   - 筛选历史记录

## 5. 简历详情页面

### 功能组件

1. **简历基本信息区**
   - 候选人姓名和基本信息
   - 联系方式（电话、邮箱）
   - 上传时间和上传者
   - 状态标签
   - 操作按钮（评估、导出、删除）

2. **简历预览区**
   - 原始简历文件预览（支持PDF、Word、图片格式）
   - 缩放控制
   - 页面导航
   - 全屏查看按钮

3. **结构化信息标签页**
   - 基本信息标签页（个人信息、联系方式）
   - 教育经历标签页（学校、专业、学历、时间段）
   - 工作经历标签页（公司、职位、时间段、职责描述）
   - 项目经历标签页（项目名称、角色、时间段、描述）
   - 技能标签页（技能名称、熟练度）
   - 证书标签页（证书名称、颁发机构、获取时间）

4. **AI评估结果区**
   - 总评分和匹配度显示（大型仪表盘）
   - 各维度评分雷达图
   - 优势和不足分析
   - AI评语和建议
   - 匹配岗位推荐

5. **岗位匹配度比较**
   - 当前应聘岗位匹配度
   - 其他潜在匹配岗位列表
   - 各岗位匹配度对比图表

6. **操作历史记录**
   - 时间轴显示简历的所有操作记录
   - 包括上传、查看、评估、修改等操作
   - 显示操作人和操作时间

7. **备注和标签**
   - 备注编辑区域（支持富文本）
   - 自定义标签添加/删除
   - 协作评论区

### 交互规范

1. **页面导航**
   - 标签页切换无刷新加载
   - 滚动时标题栏固定在顶部
   - 返回按钮返回上一页
   - 快捷键支持（方向键翻页、Esc返回）

2. **数据编辑**
   - 结构化信息支持手动修正
   - 编辑模式/查看模式切换
   - 自动保存（输入停止后1秒）
   - 修改历史记录

3. **评估交互**
   - 点击评估按钮启动/更新AI评估
   - 评估过程显示进度指示器
   - 评估完成后自动刷新结果区域
   - 支持多岗位批量评估

## 6. 岗位管理页面

### 功能组件

1. **岗位创建按钮**
   - 新建岗位按钮（主要按钮）
   - 从模板创建下拉选项
   - 批量导入按钮

2. **岗位筛选工具栏**
   - 关键词搜索框
   - 部门筛选下拉菜单
   - 状态筛选下拉菜单（招聘中、已暂停、已结束）
   - 时间范围选择器
   - 排序选项（创建时间、简历数量）

3. **岗位列表**
   - 岗位名称列
   - 部门列
   - 工作地点列
   - 招聘人数列
   - 收到简历数列（带进度条）
   - 创建时间列
   - 状态列（带状态标签）
   - 操作列（查看、编辑、暂停/激活、删除按钮）
   - 分页控件

4. **岗位统计概览**
   - 岗位总数统计
   - 各状态岗位数量分布
   - 各部门岗位数量分布
   - 简历投递量趋势图

5. **批量操作工具栏**
   - 批量删除按钮
   - 批量导出按钮
   - 批量状态更新按钮

### 交互规范

1. **创建交互**
   - 点击创建按钮打开岗位创建表单（模态框或新页面）
   - 表单分步骤填写（基本信息、岗位要求、评估设置）
   - 实时表单验证
   - 草稿自动保存

2. **列表交互**
   - 行悬停高亮
   - 点击行查看详情
   - 状态切换确认提示
   - 删除操作二次确认

3. **数据刷新**
   - 创建/编辑岗位后自动刷新列表
   - 提供手动刷新按钮
   - 状态变更后实时更新

## 7. 岗位详情/编辑页面

### 功能组件

1. **基本信息区**
   - 岗位名称输入框
   - 部门选择器
   - 工作地点输入框
   - 招聘人数输入框
   - 状态切换开关
   - 创建时间和创建人（只读）

2. **岗位描述区**
   - 富文本编辑器
   - 支持格式化、列表、图片插入
   - 字数统计
   - 模板插入功能

3. **岗位要求配置**
   - 教育要求设置（学历、专业、权重滑块）
   - 经验要求设置（年限、行业、权重滑块）
   - 技能要求设置（技能名称、等级、必要性、权重滑块）
   - 技能添加/删除按钮
   - 权重分配饼图（视觉反馈）

4. **评估维度配置**
   - 评估维度列表（维度名称、权重滑块、启用开关）
   - 自定义维度添加功能
   - 维度说明编辑器
   - 评分标准设置

5. **简历匹配设置**
   - 关键词设置（加分关键词、减分关键词）
   - 匹配算法选择
   - 匹配阈值设置
   - 自动筛选规则设置

6. **相关简历标签页**
   - 已投递简历列表
   - 评分和匹配度显示
   - 状态筛选
   - 快速查看按钮

7. **操作按钮区**
   - 保存按钮
   - 取消按钮
   - 预览按钮
   - 发布/暂停按钮
   - 复制岗位按钮

### 交互规范

1. **编辑交互**
   - 表单实时验证
   - 自动保存草稿
   - 编辑冲突检测和提示
   - 必填项视觉提示

2. **权重配置交互**
   - 拖动滑块调整权重
   - 权重总和自动计算和显示（确保总和为100%）
   - 权重变化的视觉反馈（饼图实时更新）

3. **技能配置交互**
   - 技能输入支持自动补全
   - 拖拽排序技能优先级
   - 技能标签可点击编辑

4. **保存和发布流程**
   - 保存前表单完整性验证
   - 保存成功提示
   - 发布前确认对话框
   - 发布后状态更新

## 8. AI评估页面

### 功能组件

1. **评估创建区**
   - 简历选择器（支持多选）
   - 岗位选择器
   - 评估模型选择
   - 评估维度自定义
   - 开始评估按钮

2. **评估任务列表**
   - 任务ID列
   - 简历数量列
   - 岗位名称列
   - 创建时间列
   - 状态列（带进度指示器）
   - 完成时间列
   - 操作列（查看、取消、删除按钮）

3. **评估结果列表**
   - 候选人姓名列
   - 应聘岗位列
   - 总评分列（带星级显示）
   - 匹配度列（带进度条）
   - 评估时间列
   - 操作列（查看详情、比较、导出按钮）

4. **批量操作工具栏**
   - 批量导出按钮
   - 批量删除按钮
   - 生成报告按钮

5. **评估统计概览**
   - 评估总数统计
   - 平均评分和匹配度
   - 评分分布直方图
   - 各维度平均分雷达图

### 交互规范

1. **评估创建交互**
   - 简历选择支持搜索和筛选
   - 岗位选择支持搜索
   - 评估参数实时验证
   - 开始评估后显示进度指示器

2. **评估监控交互**
   - 评估进度实时更新
   - 支持取消正在进行的评估
   - 评估完成后通知提醒
   - 失败任务重试功能

3. **结果查看交互**
   - 点击行查看详细评估结果
   - 支持多结果选择比较
   - 结果排序和筛选
   - 导出PDF/Excel格式报告

## 9. 数据分析页面

### 功能组件

1. **分析维度选择器**
   - 简历分析标签页
   - 岗位分析标签页
   - 评估分析标签页
   - 候选人画像标签页

2. **时间范围控制器**
   - 预设范围选择（今天、本周、本月、本季度、本年）
   - 自定义日期范围选择器
   - 比较周期选择（环比、同比）

3. **简历分析面板**
   - 简历来源分布饼图
   - 简历数量趋势折线图
   - 学历分布柱状图
   - 专业分布词云图
   - 工作年限分布条形图
   - 技能热度地图

4. **岗位分析面板**
   - 岗位发布趋势折线图
   - 部门岗位分布饼图
   - 简历投递热度地图
   - 岗位招聘周期分析
   - 岗位要求词云图

5. **评估分析面板**
   - 评分分布直方图
   - 各维度平均分雷达图
   - 匹配度分布热力图
   - 优势/不足词云图
   - 推荐率和淘汰率趋势图

6. **候选人画像面板**
   - 优质候选人特征分析
   - 学历-经验-评分三维散点图
   - 技能组合分析
   - 职业发展路径图
   - 地域分布地图

7. **数据导出工具**
   - 导出当前视图按钮
   - 生成分析报告按钮
   - 定期报告订阅设置

### 交互规范

1. **数据筛选交互**
   - 筛选条件变更后自动更新图表
   - 多维度交叉筛选
   - 筛选条件可保存为视图

2. **图表交互**
   - 图表悬停显示详细数据
   - 点击图表元素进行钻取分析
   - 支持缩放、平移操作
   - 图表类型切换（同一数据集）

3. **数据导出交互**
   - 选择导出格式（PDF、Excel、图片）
   - 选择导出内容（当前视图、完整报告）
   - 导出进度指示器
   - 导出完成通知

## 10. 系统设置页面

### 功能组件

1. **用户管理面板**
   - 用户列表（用户名、邮箱、角色、状态）
   - 用户创建/编辑表单
   - 角色分配控件
   - 账户状态控制
   - 密码重置功能

2. **角色权限管理面板**
   - 角色列表（角色名称、描述、用户数量）
   - 权限矩阵（功能模块 x 操作类型）
   - 权限继承关系图
   - 自定义角色创建功能

3. **部门管理面板**
   - 部门树形结构
   - 部门创建/编辑表单
   - 部门用户分配
   - 部门岗位关联

4. **AI模型配置面板**
   - 模型选择器（基础模型、高级模型）
   - API密钥配置
   - 模型参数调整（温度、最大长度等）
   - 自定义提示词模板
   - 模型测试工具

5. **系统参数配置面板**
   - 文件上传设置（类型限制、大小限制）
   - 评估维度配置（系统默认维度）
   - 评分标准配置
   - 通知设置（邮件、站内信）
   - 数据保留策略设置

6. **界面设置面板**
   - 主题选择（浅色、深色、自动）
   - 布局设置（紧凑、舒适）
   - 默认视图设置
   - 语言设置
   - 时区设置

7. **日志查看面板**
   - 操作日志列表
   - 系统日志列表
   - 日志级别筛选
   - 时间范围筛选
   - 用户筛选
   - 日志导出功能

### 交互规范

1. **设置保存交互**
   - 设置变更后显示保存按钮
   - 保存成功提示
   - 部分设置需要确认对话框
   - 支持恢复默认设置

2. **权限管理交互**
   - 权限变更二次确认
   - 权限冲突检测和提示
   - 权限预览功能
   - 批量权限分配

3. **用户管理交互**
   - 用户创建/编辑表单验证
   - 用户状态变更确认
   - 密码重置流程（发送邮件链接）
   - 用户导入/导出功能

4. **系统参数交互**
   - 参数变更影响提示
   - 敏感参数变更需管理员密码确认
   - 参数历史记录查看
   - 参数搜索功能

## 11. 个人中心页面

### 功能组件

1. **个人信息面板**
   - 头像上传/编辑
   - 基本信息编辑（姓名、职位、部门）
   - 联系信息编辑（电话、邮箱）
   - 密码修改表单

2. **通知设置面板**
   - 邮件通知设置
   - 站内信通知设置
   - 通知类型开关（系统通知、任务通知、简历通知）

3. **界面偏好设置**
   - 主题选择
   - 布局设置
   - 默认页面设置
   - 列表显示密度设置

4. **操作历史记录**
   - 登录历史
   - 操作记录列表
   - 时间范围筛选
   - 操作类型筛选

### 交互规范

1. **个人信息编辑**
   - 表单实时验证
   - 头像裁剪工具
   - 保存成功提示
   - 敏感信息修改需验证当前密码

2. **设置保存**
   - 设置实时应用
   - 设置自动保存
   - 恢复默认设置选项

## 12. 帮助中心页面

### 功能组件

1. **帮助文档浏览器**
   - 文档目录树
   - 内容搜索框
   - 文档内容显示区
   - 相关文档推荐

2. **视频教程播放器**
   - 教程分类列表
   - 视频播放器
   - 播放控制器
   - 字幕显示

3. **常见问题解答**
   - 问题分类标签
   - 问题列表（可折叠）
   - 问题搜索框
   - 问题反馈功能

4. **联系支持**
   - 问题提交表单
   - 支持类型选择
   - 文件上传功能
   - 提交历史记录

### 交互规范

1. **文档浏览交互**
   - 目录树展开/折叠
   - 文档内锚点导航
   - 搜索结果高亮
   - 文档评分反馈

2. **视频教程交互**
   - 视频播放控制
   - 播放速度调整
   - 全屏模式
   - 进度保存

3. **问题解答交互**
   - 问题展开/折叠
   - 解答有用度反馈
   - 相关问题推荐
   - 未解决问题提交
