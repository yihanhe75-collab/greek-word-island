# 希腊语单词岛 2.0

## 功能
- 图片联想卡片：每个单词支持自定义图片 URL；未添加图片时使用主题 emoji 作为视觉记忆提示。
- 希腊语朗读：使用浏览器 SpeechSynthesis，语言设为 el-GR。设备需有希腊语语音包；不同系统语音质量可能不同。
- 拉丁字母转写字段：可在添加词汇时录入，初始词条带有学习者友好转写。
- 间隔复习、小测验、单词管理、CSV 导入导出。
- PWA：支持静态托管、手机添加到主屏幕、基础离线缓存。
- Supabase 云同步：邮箱注册/登录后同步词汇和学习状态。

## 本地使用
解压后可直接打开 index.html 预览主要学习功能。浏览器的 PWA 安装/离线缓存要求 HTTPS 或 localhost。

## 发布
将本文件夹全部文件上传至 GitHub Pages、Netlify、Cloudflare Pages 等静态托管平台。不要只上传 index.html。

## 启用跨设备同步（首次设置）
1. 在 https://supabase.com/dashboard 创建项目。
2. 打开 Project Settings -> API，复制 Project URL 和 anon / publishable key。
3. 打开网站「☁️ 同步设置」，填入 URL 和 key，保存。
4. 点击「复制建表 SQL」，到 Supabase 的 SQL Editor 执行；也可以复制页面显示的 SQL。
5. 在网站注册邮箱账号。若开启邮箱确认，先确认邮件再登录。
6. 手机和电脑访问同一个网站，填入相同 Supabase URL/key，登录同一账号，点击「立即同步」。

安全说明：只在前端使用 anon/publishable key，并依赖 RLS 策略隔离用户数据。绝不可将 service_role key 放入网页。建议在 Supabase Auth 中设置合适的邮箱验证与密码策略。

## 同步策略说明
当前版本采用「合并后上传」的简化同步：首次同步会合并本地与云端单词；相同 ID 的本地记录可能覆盖云端记录。它适合个人词库的初始跨设备使用，但不是完整的实时双向冲突解决系统。建议首次跨设备使用前先导出 CSV 备份；不要在多台设备同时编辑同一词条。未来可升级为基于 updated_at 的冲突解决和自动定时同步。

## 图片
添加单词时可粘贴可公开访问的图片直链。部分图片网站禁止跨站引用；如加载失败会回退到 emoji。推荐将自有图片放在 Supabase Storage 或其他允许公开访问的静态图床。
