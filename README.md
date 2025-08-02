# Food_diary
# 家肴网站

一个美观的美食分享平台，支持菜品展示、图片上传和管理功能。

## 功能特点

- 🎨 **毛玻璃效果设计** - 现代化的UI界面
- 📸 **多图片支持** - 每个菜品可包含多张图片
- 🔍 **模糊搜索** - 支持菜品名称搜索
- 📄 **分页显示** - 大量菜品时分页展示
- 🔐 **密码保护** - 管理员密码验证
- 📤 **图片上传** - 支持拖拽上传和URL添加
- 🗂️ **菜品管理** - 添加、删除、编辑菜品

## 文件结构

```
/
├── index.html          # 主页 - 菜品展示
├── upload.php          # 管理页面 - 菜品上传和管理
├── upload_advanced.php # 图片上传处理
├── passwd_hash.php     # 密码哈希值生成工具
├── config.php          # 数据库配置
├── cdn.html            # CDN配置说明
├── css/
│   ├── index.css       # 主页样式
│   └── upload.css      # 管理页面样式
├── js/
│   ├── index.js        # 主页交互逻辑
│   └── upload.js       # 管理页面交互逻辑
└── api/
    ├── dishes.php      # 菜品API
    ├── images.php      # 图片管理API
    └── auth.php        # 认证API
```

## 安装配置

### 1. 环境要求

- PHP 7.4+
- MySQL 5.7+
- Web服务器（Apache/Nginx）

### 2. 数据库配置

1. 创建MySQL数据库：
   ```sql
   CREATE DATABASE jiayao_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   ```
2. 修改 `config.php` 中的数据库连接信息：
   ```php
   define('DB_HOST', 'localhost');
   define('DB_NAME', 'jiayao_db');
   define('DB_USER', 'your_username');
   define('DB_PASS', 'your_password');
   ```

### 3. 默认密码

系统默认管理员密码：`admin123`

如需修改密码，请使用 `passwd_hash.php` 生成新密码的哈希值，并更新数据库中的记录。

## 使用方法

### 1. 访问主页

打开 `index.html` 查看菜品展示页面：

- 支持搜索菜品名称
- 分页浏览菜品
- 多图片轮播显示

### 2. 管理菜品

访问 `upload.php` 进入管理页面：

1. **密码验证**
   - 输入管理员密码（默认：admin123）
2. **添加菜品**
   - 输入菜品名称
   - 添加备注（可选）
   - 上传图片或添加图片URL
   - 点击保存
3. **管理菜品**
   - 查看所有菜品
   - 为菜品添加更多图片
   - 删除菜品或图片

### 3. 图片上传

系统使用 `upload_advanced.php` 进行图片上传：

- 支持拖拽上传
- 支持多文件选择
- 自动上传到CDN
- 返回图片链接

## API接口

### 菜品管理

- `GET /api/dishes.php` - 获取菜品列表
- `POST /api/dishes.php` - 添加菜品
- `DELETE /api/dishes.php` - 删除菜品

### 图片管理

- `POST /api/images.php` - 添加图片
- `DELETE /api/images.php` - 删除图片

### 认证

- `POST /api/auth.php` - 验证密码

## 自定义配置

### 修改默认密码

可以通过 `passwd_hash.php` 页面生成新密码的哈希值，然后通过数据库直接修改：

```sql
UPDATE admin_password SET password_hash = '新密码哈希' WHERE id = 1;
```

### 调整分页数量

在 `index.html` 中修改：

```javascript
const params = new URLSearchParams({
    page: page,
    limit: 12,  // 修改这里的数字
    search: search
});
```

### 修改上传API

如果需要使用其他上传服务，修改 `upload.php` 中的上传URL：

```javascript
const response = await fetch('your_upload_api.php', {
    method: 'POST',
    body: formData
});
```

## 安全注意事项

1. **修改默认密码** - 首次使用后请修改默认密码
2. **数据库安全** - 使用强密码保护数据库
3. **文件权限** - 确保Web服务器有适当的文件读写权限
4. **HTTPS** - 生产环境建议使用HTTPS

## 开源协议

本项目采用 [GPL-3.0](https://gnu.ac.cn/licenses/gpl-3.0.html#license-text) 开源协议。
