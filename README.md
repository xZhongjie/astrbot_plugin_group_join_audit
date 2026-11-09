# 入群审核 · astrbot_plugin_group_join_audit

用 AstrBot 当前聊天模型自动审核 QQ 入群申请。

## 用法

群主 / 管理员在群里依次发送：

```text
/设置入群审核
/问题 你最喜欢的一本书是什么？
/参考答案 小王子        ← 可选，不设置就完全由 LLM 判断
```

之后有人申请加群时，插件会把申请人的**验证信息**交给 LLM：

- 设置了参考答案：判断验证信息是否和参考答案意思接近（不要求逐字相同）
- 没有参考答案：根据问题判断回答是否相关、认真、像正常人类申请
- 自动调用协议端 `set_group_add_request` 同意 / 拒绝

其他指令：

```text
/入群审核状态      查看当前问题、参考答案、模型
/关闭入群审核      关闭本群自动审核
/参考答案 清除     清除参考答案
```

## 安装

```bash
cd AstrBot/data/plugins
git clone https://github.com/xZhongjie/astrbot_plugin_group_join_audit.git
```

重启 AstrBot，或在 WebUI 重载插件。

## 说明

- 只支持 OneBot v11（aiocqhttp / NapCat / Lagrange）。
- 机器人必须是群主或管理员，才能自动同意 / 拒绝。
- 审核结果只写日志，不会在群里刷屏；需要人工复核时直接看 QQ 的入群申请列表。
- LLM 超时 / 返回格式异常时，插件不会自动同意或拒绝，保留给管理员人工处理。
- 配置里的 `provider_id` 可以指定审核用的模型，留空使用当前会话模型；建议选小模型。

## 配置

| 配置项 | 默认值 | 说明 |
| --- | --- | --- |
| `provider_id` | 空 | 审核使用的聊天模型，留空用当前会话模型 |
| `review_timeout` | `30` | LLM 超时秒数 |

## License

[MIT](LICENSE)
