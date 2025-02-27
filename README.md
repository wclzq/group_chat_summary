# Group Chat Summary Plugin

群聊总结插件 (group_chat_summary) 是一个用于自动记录和总结群聊内容的插件。它能够实时保存群聊记录，并根据需要生成结构化的群聊总结报告。

## 功能特点

- 自动记录群聊消息
- 生成结构化的群聊总结报告
- 支持自定义总结消息数量
- 支持黑名单功能
- 自动清理过期消息

## 下载安装
```
#installp https://github.com/wclzq/group_chat_summary.git
```
然后#scanp扫描
或者下载文件放到plugins目录下，并配置config.json

## 使用方法

在群聊中，发送以下命令来获取群聊总结：

例如：
- `总结聊天 30` - 总结最近30条消息
- `总结聊天` - 使用默认数量(99条)进行总结

## 总结报告格式

总结报告包含以下内容：
1. 群聊整体风格评价
2. 按热度排序的话题列表，每个话题包含：
   - 话题名称（带序号emoji）
   - 热度（用🔥表示）
   - 参与者（最多5人）
   - 讨论时间段
   - 讨论过程
   - 话题评价
3. 最活跃的前五名发言者统计

## 配置参数

在 `config.json` 中配置以下参数：

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| open_ai_api_base | string | OpenAI API的基础URL | 必填 |
| open_ai_api_key | string | OpenAI API密钥 | 必填 |
| open_ai_model | string | 使用的OpenAI模型 | "gpt-4o-mini" |
| max_record_quantity | number | 每个群保存的最大消息数量 | 1000 |
| black_chat_name | array | 黑名单用户列表 | [] |

配置示例：

```json
{
  "open_ai_api_base": "http://your-api-base-url/v1",
  "open_ai_api_key": "your-api-key",
  "open_ai_model": "gpt-4o-mini",
  "max_record_quantity": 1000,
  "black_chat_name": ["群聊1", "群聊2"]
}
```

## 数据存储

插件使用SQLite数据库存储聊天记录，数据库文件名为 `chat_records.db`。数据会自动清理，只保留每个群的最新消息（数量由 max_record_quantity 配置）。

## 注意事项

1. 确保已正确配置OpenAI API相关参数
2. 插件仅支持群聊总结，私聊不可用
3. 被加入黑名单的群聊无法使用总结功能
4. 建议根据服务器性能适当调整 max_record_quantity 参数

## 错误处理

如果遇到"模型请求失败了，呵呵"的提示，请检查：
1. API配置是否正确
2. 网络连接是否正常
3. API密钥是否有效

## 作者信息

- 插件名称：group_chat_summary
- 版本：0.1
- 作者：wangcl
