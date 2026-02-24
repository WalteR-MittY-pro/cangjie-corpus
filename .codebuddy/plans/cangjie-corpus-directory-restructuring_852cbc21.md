---
name: cangjie-corpus-directory-restructuring
overview: 为仓颉语料仓库设计MCP可检索的目录结构方案
todos:
  - id: analysis-summary
    content: 分析总结当前仓库结构和内容特点
    status: completed
  - id: propose-directory-structure
    content: 提出面向MCP检索优化的目录重组建议方案
    status: completed
  - id: detail-naming-convention
    content: 详细说明命名规范和层级结构
    status: completed
---

## 用户需求

当前仓库作为仓颉语料输入，但目录组织方式较差，目录名称与文档内容不相关，导致MCP检索无法有效索引。需要提供MCP可检索的良好目录格式建议方案。

## 现有仓库结构

- extra/ (12个文件): 基础数据类型和集合简明文档
- libs/std/ (247个文件): 仓颉标准库API文档
- libs/stdx/ (114个文件): 仓颉扩展库文档
- manual/source_zh_cn/ (105个md): 仓颉编程手册
- ohos/zh-cn/ (649个文件): OpenHarmony应用开发文档
- tools/ (16个md): 工具文档

## 核心问题

1. 目录名称抽象（extra/libs/manual）与内容不匹配
2. 文档命名混用中英文
3. 缺乏面向MCP检索的分类体系

## 技术方案

### 目录重组原则

1. **语义化目录命名**: 目录名称应直接反映内容主题，使用中文命名便于中文MCP检索
2. **层级分类清晰**: 建立"领域-子领域-具体API/概念"的三级分类体系
3. **命名一致性**: 统一使用中文命名，文件名包含关键语义词汇

### 建议的目录结构

```
cangjie-corpus/
├── 01_编程语言基础/
│   ├── 01_数据类型/
│   │   ├── 基础数据类型.md (Int64, Float64, Bool, Rune, String)
│   │   ├── 数组Array.md
│   │   ├── 集合List.md
│   │   ├── 集合Map.md
│   │   ├── 集合Set.md
│   │   └── 元组Tuple.md
│   ├── 02_语法特性/
│   │   ├── 函数定义.md
│   │   ├── 流程控制.md
│   │   ├── 模式匹配.md
│   │   └── 泛型.md
│   └── 03_面向对象/
│       ├── 类定义.md
│       ├── 接口定义.md
│       ├── 继承与多态.md
│       └── 扩展.md
│
├── 02_标准库API/
│   ├── 集合库collection/
│   │   ├── ArrayList.md
│   │   ├── HashMap.md
│   │   ├── HashSet.md
│   │   └── Sorting.md
│   ├── 输入输出io/
│   ├── 文件系统fs/
│   ├── 网络库net/
│   ├── 正则表达式regex/
│   ├── 时间库time/
│   ├── 单元测试unittest/
│   └── 反射库reflect/
│
├── 03_扩展库stdx/
│
├── 04_编程手册/
│   ├── 基础概念first_understanding/
│   ├── 基本数据类型basic_data_type/
│   ├── 集合collections/
│   ├── 函数function/
│   ├── 类与接口class_and_interface/
│   ├── 并发concurrency/
│   ├── 错误处理error_handle/
│   ├── 宏Macro/
│   └── 包管理package/
│
├── 05_OpenHarmony开发/
│   ├── 快速入门cj-start/
│   ├── 应用模型application-models/
│   ├── UI框架arkui-cj/
│   │   ├── 布局组件.md
│   │   ├── 基础组件.md
│   │   ├── 动画.md
│   │   └── 事件处理.md
│   ├── 数据管理database/
│   │   ├── 键值存储.md
│   │   ├── 关系型数据库.md
│   │   └── 数据加密.md
│   ├── 网络连接connectivity/
│   ├── 媒体服务media/
│   ├── 文件管理file-management/
│   └── 设备管理device/
│
└── 06_工具与生态/
    ├── 开发工具tools/
    └── 三方库libs/
```

### MCP检索优化策略

1. **文件名语义化**: 每个文件名应包含核心关键词，如"仓颉Array数组使用方法.md"
2. **Frontmatter元数据**: 在每个md文件头部添加便于检索的元信息
3. **目录层级深度控制**: 控制在3层以内，避免过深影响检索效率
4. **同义词汇整理**: 整理常用同义词到别名映射文件