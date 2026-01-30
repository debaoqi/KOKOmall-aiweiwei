# KOKO Mall PWA

这是一个完整的渐进式Web应用（PWA）版本。

## 文件结构

```
pwa-dist/
├── index.html          # 主应用文件
├── manifest.json       # PWA清单文件
├── sw.js              # Service Worker（离线支持）
├── icon-192.png       # 192x192应用图标
├── icon-512.png       # 512x512应用图标
├── koko-logo.svg      # SVG格式的logo
└── README.md          # 本文件
```

## 安装说明

### 1. 生成图标文件

如果图标文件（icon-192.png 和 icon-512.png）不存在，请：

**方法1：使用在线工具**
- 访问 https://realfavicongenerator.net/
- 上传 koko-logo.svg 或创建新图标
- 下载生成的PNG图标文件
- 重命名为 icon-192.png 和 icon-512.png

**方法2：使用图形软件**
- 使用 Photoshop、GIMP 或其他图像编辑软件
- 创建 192x192 和 512x512 像素的PNG文件
- 背景色：#FFA500（橙色）
- 文字：KOKO（黑色 #1C1C1C）
- 保存为 icon-192.png 和 icon-512.png

**方法3：使用命令行工具**
```bash
# 如果有ImageMagick
convert -size 192x192 xc:#FFA500 -gravity center -pointsize 60 -fill "#1C1C1C" -font Arial-Bold -annotate +0+0 "KOKO" icon-192.png
convert -size 512x512 xc:#FFA500 -gravity center -pointsize 160 -fill "#1C1C1C" -font Arial-Bold -annotate +0+0 "KOKO" icon-512.png
```

### 2. 部署

**本地测试：**
```bash
# 使用Python简单HTTP服务器
cd pwa-dist
python3 -m http.server 8000

# 或使用Node.js http-server
npx http-server pwa-dist -p 8000
```

然后在浏览器访问：http://localhost:8000

**部署到服务器：**
1. 将所有文件上传到Web服务器
2. 确保服务器支持HTTPS（PWA要求）
3. 访问网站，浏览器会提示"添加到主屏幕"

### 3. 功能特性

- ✅ 离线支持（Service Worker）
- ✅ 可安装到主屏幕
- ✅ 响应式设计
- ✅ 快速加载
- ✅ 缓存策略优化

## 配置说明

### manifest.json
- `name`: 应用完整名称
- `short_name`: 简短名称（主屏幕显示）
- `theme_color`: 主题色（#FFA500 橙色）
- `background_color`: 启动画面背景色
- `display`: standalone（独立应用模式）

### sw.js
Service Worker配置了以下缓存策略：
- 安装时缓存关键资源
- 激活时清理旧缓存
- 网络优先，缓存备用

## 浏览器支持

- Chrome/Edge: 完全支持
- Safari (iOS 11.3+): 支持
- Firefox: 支持
- Opera: 支持

## 注意事项

1. **HTTPS要求**：PWA必须在HTTPS环境下运行（localhost除外）
2. **图标文件**：确保icon-192.png和icon-512.png存在
3. **Service Worker**：首次访问时会自动注册
4. **更新机制**：修改sw.js中的CACHE_NAME版本号可强制更新缓存

## 更新应用

要更新已安装的PWA：
1. 修改sw.js中的CACHE_NAME版本号（如：koko-mall-v2）
2. 用户重新访问网站时会自动更新
3. 或手动清除浏览器缓存

## 故障排除

**图标不显示：**
- 检查icon-192.png和icon-512.png是否存在
- 检查manifest.json中的路径是否正确

**Service Worker未注册：**
- 检查sw.js文件是否存在
- 检查浏览器控制台错误信息
- 确保在HTTPS或localhost环境下

**无法安装：**
- 确保manifest.json格式正确
- 确保有有效的图标文件
- 检查浏览器是否支持PWA
