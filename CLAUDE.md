# VideoGet 项目开发规则

## 项目概述
VideoGet - 万能视频下载器，前后端分离架构

## 技术栈
- **前端**: Vue 3 + Tailwind CSS + Vite
- **后端**: Python 3.11 + FastAPI + yt-dlp
- **部署**: Docker + Docker Compose

## 开发规范

### 分支管理
- `main`: 主分支，稳定版本，禁止直接提交
- `develop`: 开发分支，功能合并到此
- `feature/*`: 功能分支，从 develop 切出
- `hotfix/*`: 紧急修复分支

### 代码规范
1. **前端**
   - 使用 Composition API
   - Tailwind 类名按布局→外观→交互排序
   - 组件名使用 PascalCase

2. **后端**
   - 遵循 PEP 8
   - 使用类型注解
   - API 路由使用 async/await

### 修改原则
1. 不修改现有功能的核心逻辑，除非必要
2. 新增功能优先创建新文件，而非修改旧文件
3. 修改前先备份或确认可回滚
4. 保持设计系统一致性（蓝色科技风）

### 禁止操作
- 直接修改 main 分支
- 删除或重命名现有 API 端点
- 修改现有数据库模型（如后续添加）
- 提交敏感信息（API 密钥、密码等）

### 建议操作
- 使用 Git 进行版本控制
- 每次开发前创建功能分支
- 定期提交代码（commit）
- 开发完成后进行测试验证
