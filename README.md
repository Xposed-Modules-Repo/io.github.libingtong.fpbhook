# 发票盒子 VIP

针对 **发票盒子**（`com.quickwis.fapiaohezi`）的会员功能增强模块，基于 libxposed API 102。

## 功能

- PDF 导出清晰度：解除强制标准清晰度限制
- 三张 / 四张 A4 拼版打印
- 标签数量限制解除
- 批量选择发票超过 10 张
- 单张发票关联附单上限（3 → 20）
- 抬头筛选限制解除
- 通用附单模板保存
- 默认收票邮箱（系统 / 别名 / 自定义）
- 会员卡片与到期时间显示

## 兼容性

- Xposed API：libxposed **102**（要求 LSPosed 1.9.0+）
- Android 8.0+（minSdk 26）
- 目标应用：发票盒子 1.97.7 实测通过

**跨版本设计**：模块不依赖任何混淆后的类名或方法名。定位锚点是业务包内的 `VipInfoBean` 实体类，配合按 `versionCode` 的定位缓存与 dex 全量深度扫描，应用升级后无需模块更新即可继续工作。

## 使用

1. 安装本模块
2. 在 LSPosed 中启用，作用域勾选「发票盒子」
3. 强制停止发票盒子后重新打开

## 设置

模块打开后提供「隐藏桌面图标」开关，隐藏后模块照常工作。

也可以用 adb：

```bash
adb shell am start -n io.github.libingtong.fpbhook/.MainActivity --ez hide true  -f 0x20000000
adb shell am start -n io.github.libingtong.fpbhook/.MainActivity --ez hide false -f 0x20000000
```

## 日志

```bash
adb logcat -s LSPosedFramework | grep FpbHook
```

## 已知限制

以下两项由服务端判定，客户端模块无法改变：

- 自定义归类数量
- Excel 每月试用次数

服务端会返回 `-2000 / -2001 / -2002`，客户端仅透传错误码。

## 源码

https://github.com/libingtong/lsposed-fpb-hook
