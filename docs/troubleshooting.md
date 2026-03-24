# Make Scenario 6: Property Image Processing 自动化配置详解

## **触发条件:**
- Google Sheets 新行触发（含房源完整信息、图片ID、文案等）

## **主要步骤:**

### 1. Google Sheets - Watch Rows
- Spreadsheet ID: `1AMEj3SIYP-ofxRCEq4zlDRgFL-ilijPEyUMIRayMFUs`
- Sheet Name: `Temp_Property_Input`
- Limit: 1

### 2. Filter (Router)
条件（AND）：
- `gemini_result` Exists
- `all_copy_result` Exists
- `hero_image_url` Exists
- `image_status` is empty

### 3. Text Parser (Regex)
提取这些字段：

| 字段名 | 正则表达式 |
|--------|-----------|
| project_name | Project \/ Property Name:\s*([^\n]+) |
| area | Area:\s*([^\n]+) |
| property_type | Property Type:\s*([^\n]+) |
| price_text | Price:\s*([RM0-9k.]+) |
| bedrooms | Bedrooms:\s*([0-9]+) |
| bathrooms | Bathrooms:\s*([0-9]+) |
| renovation | Renovation:\s*([^\n]+) |
| special_points | Special Selling Points:\s*([^\n]+) |
| nearby | Nearby:\s*([^\n]+) |

### 4. 清理价格
- 输入：price_text
- 替换：删除所有非数字字符
- 输出：price_numeric

### 5. 判断风格
- 如果 price_numeric < 500000：使用温暖棕色 (#D4A574)
- 否则：使用深蓝色 (#1E3A5F)

### 6-7. 生成图片 + 添加文字
- 基础尺寸：1200x800
- 添加项目名、地区、价格、房型、房间数、特点、附近

### 8. Array Iterator (循环 3 个尺寸)

### 9. 调整尺寸 + 添加水印
- 为每个平台调整到对应尺寸
- 添加水印：Martin Toh (TRR-EAG) + 0104649768
- 添加两个 Logo（TRR + EAG）

### 10. 上传到 Google Drive
- 文件夹：property_images/{date}/
- 文件名：property_{temp_id}_{platform}_{date}.png

### 11. 更新 Google Sheet
- 写入三个图片 URL
- 设置 image_status = completed

### 12. Telegram 通知（可选）
- 发送处理完成消息
- 包含三个平台的图片链接
