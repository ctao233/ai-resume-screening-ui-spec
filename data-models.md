# AI简历筛选系统 - 数据模型规范

本文档详细描述了AI简历筛选系统的核心数据模型，包括各实体的属性、关系和数据流向，为UI设计和前端开发提供数据结构参考。

## 目录

1. [用户相关模型](#1-用户相关模型)
2. [简历相关模型](#2-简历相关模型)
3. [岗位相关模型](#3-岗位相关模型)
4. [评估相关模型](#4-评估相关模型)
5. [系统配置模型](#5-系统配置模型)
6. [数据分析模型](#6-数据分析模型)
7. [实体关系图](#7-实体关系图)

## 1. 用户相关模型

### 1.1 用户模型 (User)

```json
{
  "id": "用户唯一标识符",
  "username": "用户名",
  "email": "电子邮箱",
  "phone": "手机号码",
  "name": "真实姓名",
  "avatar": "头像URL",
  "position": "职位",
  "departmentId": "部门ID",
  "roleIds": ["角色ID数组"],
  "status": "状态(active/inactive)",
  "lastLoginTime": "最后登录时间",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 1.2 角色模型 (Role)

```json
{
  "id": "角色唯一标识符",
  "name": "角色名称",
  "description": "角色描述",
  "permissions": [
    {
      "module": "模块名称",
      "actions": ["view", "create", "edit", "delete"]
    }
  ],
  "isSystem": "是否系统预设角色",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 1.3 部门模型 (Department)

```json
{
  "id": "部门唯一标识符",
  "name": "部门名称",
  "code": "部门编码",
  "parentId": "上级部门ID",
  "path": "部门路径(例如/1/2/3)",
  "level": "部门层级",
  "managerUserId": "部门负责人ID",
  "description": "部门描述",
  "status": "状态(active/inactive)",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 1.4 用户通知设置模型 (UserNotificationSetting)

```json
{
  "userId": "用户ID",
  "settings": {
    "inApp": {
      "newResume": true,
      "evaluationComplete": true,
      "systemAnnouncement": true,
      "taskReminder": true
    },
    "email": {
      "newResume": false,
      "evaluationComplete": true,
      "systemAnnouncement": false,
      "weeklyReport": true,
      "monthlyReport": true
    },
    "sms": {
      "urgentNotice": true,
      "securityVerification": true
    }
  },
  "updatedAt": "更新时间"
}
```

### 1.5 用户界面设置模型 (UserInterfaceSetting)

```json
{
  "userId": "用户ID",
  "theme": "主题(light/dark/system)",
  "colorScheme": "颜色方案",
  "fontSize": "字体大小(small/medium/large)",
  "density": "列表密度(compact/normal/comfortable)",
  "defaultHomePage": "默认首页路径",
  "dashboardLayout": [
    {
      "id": "组件ID",
      "type": "组件类型",
      "position": {"x": 0, "y": 0, "w": 6, "h": 4}
    }
  ],
  "updatedAt": "更新时间"
}
```

## 2. 简历相关模型

### 2.1 简历模型 (Resume)

```json
{
  "id": "简历唯一标识符",
  "fileName": "原始文件名",
  "fileType": "文件类型(pdf/doc/docx/jpg)",
  "fileSize": "文件大小(字节)",
  "fileUrl": "文件存储URL",
  "uploadUserId": "上传用户ID",
  "source": "简历来源",
  "parseStatus": "解析状态(pending/processing/completed/failed)",
  "parseErrorMsg": "解析错误信息",
  "candidateInfo": {
    "name": "候选人姓名",
    "gender": "性别",
    "age": "年龄",
    "phone": "联系电话",
    "email": "电子邮箱",
    "currentStatus": "当前状态(未联系/已联系/面试中/已录用/已拒绝)",
    "highestEducation": "最高学历",
    "graduateSchool": "毕业院校",
    "currentCompany": "当前/最近工作单位",
    "currentPosition": "当前/最近职位",
    "workYears": "工作年限",
    "expectedPosition": "期望岗位",
    "expectedSalary": "期望薪资"
  },
  "educations": [
    {
      "school": "学校名称",
      "major": "专业",
      "degree": "学历",
      "startDate": "入学时间",
      "endDate": "毕业时间",
      "description": "教育经历描述"
    }
  ],
  "workExperiences": [
    {
      "company": "公司名称",
      "position": "职位",
      "startDate": "开始时间",
      "endDate": "结束时间",
      "description": "工作描述"
    }
  ],
  "projectExperiences": [
    {
      "name": "项目名称",
      "role": "担任角色",
      "startDate": "开始时间",
      "endDate": "结束时间",
      "description": "项目描述",
      "technologies": ["技术栈"]
    }
  ],
  "skills": [
    {
      "name": "技能名称",
      "level": "掌握程度(了解/熟悉/精通)",
      "years": "使用年限"
    }
  ],
  "certificates": [
    {
      "name": "证书名称",
      "issueDate": "获取时间",
      "expiryDate": "有效期"
    }
  ],
  "tags": ["标签数组"],
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 2.2 简历操作记录模型 (ResumeActivity)

```json
{
  "id": "记录唯一标识符",
  "resumeId": "简历ID",
  "userId": "操作用户ID",
  "actionType": "操作类型(upload/parse/evaluate/edit/status_change)",
  "actionDetail": "操作详情",
  "createdAt": "创建时间"
}
```

## 3. 岗位相关模型

### 3.1 岗位模型 (Job)

```json
{
  "id": "岗位唯一标识符",
  "title": "岗位名称",
  "departmentId": "部门ID",
  "locations": ["工作地点数组"],
  "headcount": "招聘人数",
  "jobType": "工作性质(全职/兼职/实习)",
  "salaryRange": {
    "min": "最低薪资",
    "max": "最高薪资",
    "currency": "货币单位",
    "period": "计薪周期(月/年)"
  },
  "status": "岗位状态(draft/active/paused/closed)",
  "description": "岗位描述(富文本)",
  "responsibilities": ["岗位职责数组"],
  "requirements": {
    "education": ["学历要求数组"],
    "workYears": {"min": "最小工作年限", "max": "最大工作年限"},
    "languages": [
      {
        "name": "语言名称",
        "level": "熟练程度"
      }
    ],
    "skills": [
      {
        "name": "技能名称",
        "level": "要求级别(了解/熟悉/精通)",
        "isRequired": "是否必要技能"
      }
    ],
    "certificates": [
      {
        "name": "证书名称",
        "isRequired": "是否必要证书"
      }
    ],
    "others": ["其他要求数组"]
  },
  "evaluationSettings": {
    "weights": {
      "education": "教育背景权重(0-100)",
      "workExperience": "工作经验权重(0-100)",
      "skills": "技能匹配权重(0-100)",
      "projectExperience": "项目经验权重(0-100)"
    },
    "thresholds": {
      "high": "高匹配度阈值(默认80)",
      "medium": "中匹配度阈值(默认60)",
      "low": "低匹配度阈值(默认40)"
    },
    "autoRules": [
      {
        "condition": {
          "type": "匹配度/技能/工作年限/学历",
          "operator": ">/</=/!=/>=/<=/in/not in",
          "value": "条件值"
        },
        "action": "通过/拒绝",
        "logic": "and/or"
      }
    ]
  },
  "createdUserId": "创建用户ID",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 3.2 岗位模板模型 (JobTemplate)

```json
{
  "id": "模板唯一标识符",
  "name": "模板名称",
  "category": "模板分类",
  "description": "模板描述",
  "jobData": "岗位模型数据(不含ID和时间字段)",
  "isSystem": "是否系统预设模板",
  "createdUserId": "创建用户ID",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

## 4. 评估相关模型

### 4.1 评估任务模型 (Evaluation)

```json
{
  "id": "评估唯一标识符",
  "resumeId": "简历ID",
  "jobId": "岗位ID",
  "status": "评估状态(pending/processing/completed/failed)",
  "priority": "优先级(low/medium/high)",
  "errorMessage": "错误信息",
  "progress": "评估进度(0-100)",
  "result": {
    "overallScore": "总体匹配度分数(0-100)",
    "matchLevel": "匹配等级(high/medium/low)",
    "percentileRank": "百分位排名",
    "dimensionScores": {
      "education": "教育背景评分(0-100)",
      "workExperience": "工作经验评分(0-100)",
      "skills": "技能匹配评分(0-100)",
      "projectExperience": "项目经验评分(0-100)"
    },
    "strengths": [
      {
        "aspect": "优势方面",
        "description": "详细说明",
        "evidence": "支持证据"
      }
    ],
    "weaknesses": [
      {
        "aspect": "不足方面",
        "description": "详细说明",
        "suggestion": "改进建议"
      }
    ],
    "skillMatches": [
      {
        "name": "技能名称",
        "requiredLevel": "要求级别",
        "candidateLevel": "候选人级别",
        "gap": "差距分析",
        "score": "匹配分数(0-100)"
      }
    ],
    "interviewSuggestions": {
      "questions": [
        {
          "category": "问题类别",
          "question": "问题内容",
          "expectedPoints": ["预期答案要点"]
        }
      ],
      "focusAreas": ["重点关注领域"]
    }
  },
  "createdUserId": "创建用户ID",
  "createdAt": "创建时间",
  "completedAt": "完成时间",
  "updatedAt": "更新时间"
}
```

### 4.2 评估历史模型 (EvaluationHistory)

```json
{
  "id": "历史记录唯一标识符",
  "resumeId": "简历ID",
  "jobId": "岗位ID",
  "evaluationId": "评估ID",
  "overallScore": "总体匹配度分数(0-100)",
  "dimensionScores": {
    "education": "教育背景评分(0-100)",
    "workExperience": "工作经验评分(0-100)",
    "skills": "技能匹配评分(0-100)",
    "projectExperience": "项目经验评分(0-100)"
  },
  "createdAt": "创建时间"
}
```

## 5. 系统配置模型

### 5.1 系统参数模型 (SystemConfig)

```json
{
  "aiModel": {
    "resumeParsingModel": "简历解析模型",
    "evaluationModel": "评估模型",
    "recommendationModel": "推荐模型",
    "modelParams": {
      "accuracy": "精度级别(high/medium/low)",
      "speed": "速度级别(fast/normal/slow)"
    }
  },
  "fileUpload": {
    "allowedTypes": ["允许的文件类型数组"],
    "maxSize": "最大文件大小(字节)",
    "storageLocation": "存储位置"
  },
  "emailNotification": {
    "smtpServer": "SMTP服务器",
    "smtpPort": "SMTP端口",
    "username": "用户名",
    "password": "密码(加密)",
    "senderEmail": "发件人邮箱",
    "senderName": "发件人名称"
  },
  "dataRetention": {
    "resumeRetentionDays": "简历保留天数",
    "evaluationRetentionDays": "评估结果保留天数",
    "activityLogRetentionDays": "操作日志保留天数"
  },
  "evaluationDimensions": [
    {
      "id": "维度ID",
      "name": "维度名称",
      "description": "维度描述",
      "defaultWeight": "默认权重",
      "isActive": "是否启用"
    }
  ],
  "updatedUserId": "更新用户ID",
  "updatedAt": "更新时间"
}
```

### 5.2 系统公告模型 (SystemAnnouncement)

```json
{
  "id": "公告唯一标识符",
  "title": "公告标题",
  "content": "公告内容(富文本)",
  "type": "公告类型(info/warning/error/maintenance)",
  "priority": "优先级(low/medium/high)",
  "startTime": "生效开始时间",
  "endTime": "生效结束时间",
  "isActive": "是否激活",
  "targetUserIds": ["目标用户ID数组(为空表示所有用户)"],
  "targetRoleIds": ["目标角色ID数组(为空表示所有角色)"],
  "createdUserId": "创建用户ID",
  "createdAt": "创建时间",
  "updatedAt": "更新时间"
}
```

### 5.3 操作日志模型 (ActivityLog)

```json
{
  "id": "日志唯一标识符",
  "userId": "操作用户ID",
  "username": "操作用户名",
  "ipAddress": "IP地址",
  "userAgent": "用户代理",
  "module": "操作模块",
  "action": "操作类型",
  "resourceType": "资源类型",
  "resourceId": "资源ID",
  "detail": "操作详情",
  "status": "操作状态(success/failure)",
  "errorMessage": "错误信息",
  "createdAt": "创建时间"
}
```

## 6. 数据分析模型

### 6.1 数据概览模型 (AnalyticsOverview)

```json
{
  "timeRange": {
    "start": "开始时间",
    "end": "结束时间",
    "type": "时间范围类型(day/week/month/quarter/year/custom)"
  },
  "comparison": {
    "previousStart": "上一时间段开始时间",
    "previousEnd": "上一时间段结束时间"
  },
  "metrics": {
    "resumeCount": {
      "current": "当前时间段简历总数",
      "previous": "上一时间段简历总数",
      "change": "变化百分比"
    },
    "evaluationCount": {
      "current": "当前时间段评估总数",
      "previous": "上一时间段评估总数",
      "change": "变化百分比"
    },
    "averageMatchRate": {
      "current": "当前时间段平均匹配度",
      "previous": "上一时间段平均匹配度",
      "change": "变化百分比"
    },
    "interviewConversionRate": {
      "current": "当前时间段面试转化率",
      "previous": "上一时间段面试转化率",
      "change": "变化百分比"
    },
    "recruitmentEfficiency": {
      "current": "当前时间段招聘效率(天)",
      "previous": "上一时间段招聘效率(天)",
      "change": "变化百分比"
    }
  }
}
```

### 6.2 简历分析模型 (ResumeAnalytics)

```json
{
  "timeRange": {
    "start": "开始时间",
    "end": "结束时间"
  },
  "sourceAnalysis": {
    "distribution": [
      {
        "source": "来源名称",
        "count": "简历数量",
        "percentage": "百分比"
      }
    ],
    "trend": [
      {
        "date": "日期",
        "sources": [
          {
            "source": "来源名称",
            "count": "简历数量"
          }
        ]
      }
    ]
  },
  "qualityAnalysis": {
    "matchRateDistribution": [
      {
        "range": "匹配度区间",
        "count": "简历数量",
        "percentage": "百分比"
      }
    ],
    "sourceQuality": [
      {
        "source": "来源名称",
        "averageMatchRate": "平均匹配度"
      }
    ]
  },
  "processingEfficiency": {
    "timeDistribution": [
      {
        "range": "处理时间区间(小时)",
        "count": "简历数量",
        "percentage": "百分比"
      }
    ],
    "statusCounts": [
      {
        "status": "状态名称",
        "count": "简历数量",
        "percentage": "百分比"
      }
    ]
  }
}
```

### 6.3 岗位分析模型 (JobAnalytics)

```json
{
  "timeRange": {
    "start": "开始时间",
    "end": "结束时间"
  },
  "recruitmentStatus": [
    {
      "jobId": "岗位ID",
      "jobTitle": "岗位名称",
      "department": "部门名称",
      "resumeCount": "简历数量",
      "evaluatedCount": "已评估数量",
      "interviewedCount": "已面试数量",
      "hiredCount": "已录用数量",
      "averageMatchRate": "平均匹配度"
    }
  ],
  "trendAnalysis": {
    "dates": ["日期数组"],
    "jobs": [
      {
        "jobId": "岗位ID",
        "jobTitle": "岗位名称",
        "counts": ["每日简历数量数组"]
      }
    ]
  },
  "difficultyAnalysis": [
    {
      "jobId": "岗位ID",
      "jobTitle": "岗位名称",
      "difficultyIndex": "难填度指数(0-100)",
      "factors": [
        {
          "factor": "因素名称",
          "impact": "影响程度(0-100)"
        }
      ]
    }
  ]
}
```

### 6.4 候选人分析模型 (CandidateAnalytics)

```json
{
  "timeRange": {
    "start": "开始时间",
    "end": "结束时间"
  },
  "demographicProfile": {
    "educationDistribution": [
      {
        "education": "学历级别",
        "count": "候选人数量",
        "percentage": "百分比"
      }
    ],
    "workYearsDistribution": [
      {
        "range": "工作年限区间",
        "count": "候选人数量",
        "percentage": "百分比"
      }
    ],
    "skillHeatmap": [
      {
        "skill": "技能名称",
        "count": "候选人数量",
        "percentage": "百分比"
      }
    ],
    "locationDistribution": [
      {
        "location": "地区名称",
        "count": "候选人数量",
        "percentage": "百分比",
        "coordinates": {"lat": "纬度", "lng": "经度"}
      }
    ]
  },
  "highQualityCandidateAnalysis": {
    "commonTraits": [
      {
        "trait": "特征名称",
        "frequency": "出现频率",
        "importance": "重要性分数"
      }
    ],
    "skillCombinations": [
      {
        "skills": ["技能组合"],
        "count": "候选人数量",
        "averageMatchRate": "平均匹配度"
      }
    ],
    "experienceBackground": [
      {
        "background": "背景类型",
        "count": "候选人数量",
        "percentage": "百分比"
      }
    ]
  },
  "attritionAnalysis": {
    "stageAttritionRates": [
      {
        "stage": "阶段名称",
        "count": "流失数量",
        "rate": "流失率"
      }
    ],
    "attritionReasons": [
      {
        "reason": "原因类别",
        "count": "数量",
        "percentage": "百分比"
      }
    ]
  }
}
```

### 6.5 评估分析模型 (EvaluationAnalytics)

```json
{
  "timeRange": {
    "start": "开始时间",
    "end": "结束时间"
  },
  "scoreDistribution": {
    "overall": [
      {
        "range": "分数区间",
        "count": "评估数量",
        "percentage": "百分比"
      }
    ],
    "dimensions": [
      {
        "dimension": "维度名称",
        "distribution": [
          {
            "range": "分数区间",
            "count": "评估数量",
            "percentage": "百分比"
          }
        ]
      }
    ]
  },
  "dimensionCorrelation": [
    {
      "dimension": "维度名称",
      "correlationWithHiring": "与录用决策的相关性(-1到1)",
      "importance": "重要性排名"
    }
  ],
  "evaluationAccuracy": {
    "overallAccuracy": "总体准确率",
    "falsePositiveRate": "误判率(高估)",
    "falseNegativeRate": "漏判率(低估)",
    "accuracyTrend": [
      {
        "date": "日期",
        "accuracy": "准确率"
      }
    ]
  }
}
```

## 7. 实体关系图

以下是系统主要实体之间的关系描述：

```
用户(User) --1:N--> 简历(Resume)：用户可以上传多个简历
用户(User) --N:N--> 角色(Role)：用户可以拥有多个角色，角色可以分配给多个用户
用户(User) --N:1--> 部门(Department)：用户属于一个部门，部门包含多个用户
部门(Department) --1:N--> 岗位(Job)：部门可以发布多个岗位
部门(Department) --1:N--> 部门(Department)：部门可以有多个子部门

简历(Resume) --1:N--> 评估(Evaluation)：一份简历可以针对多个岗位进行评估
岗位(Job) --1:N--> 评估(Evaluation)：一个岗位可以评估多份简历
评估(Evaluation) --1:1--> 评估历史(EvaluationHistory)：每次评估会生成一条历史记录

简历(Resume) --1:N--> 简历操作记录(ResumeActivity)：一份简历可以有多条操作记录
用户(User) --1:N--> 简历操作记录(ResumeActivity)：用户可以对多份简历进行操作

用户(User) --1:1--> 用户通知设置(UserNotificationSetting)：每个用户有一个通知设置
用户(User) --1:1--> 用户界面设置(UserInterfaceSetting)：每个用户有一个界面设置

岗位(Job) --N:1--> 岗位模板(JobTemplate)：多个岗位可以基于同一个模板创建
```

---

## 附录：数据字典

### 用户状态 (UserStatus)
- active: 启用
- inactive: 禁用

### 简历解析状态 (ResumeParseStatus)
- pending: 待解析
- processing: 解析中
- completed: 已完成
- failed: 解析失败

### 候选人状态 (CandidateStatus)
- uncontacted: 未联系
- contacted: 已联系
- interviewing: 面试中
- hired: 已录用
- rejected: 已拒绝

### 岗位状态 (JobStatus)
- draft: 草稿
- active: 招聘中
- paused: 已暂停
- closed: 已关闭

### 评估状态 (EvaluationStatus)
- pending: 等待中
- processing: 评估中
- completed: 已完成
- failed: 失败

### 匹配等级 (MatchLevel)
- high: 高匹配度
- medium: 中匹配度
- low: 低匹配度

### 技能级别 (SkillLevel)
- basic: 了解
- proficient: 熟悉
- expert: 精通

### 学历级别 (EducationLevel)
- highSchool: 高中
- juniorCollege: 大专
- bachelor: 本科
- master: 硕士
- doctor: 博士
- postdoc: 博士后
