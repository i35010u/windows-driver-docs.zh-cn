---
title: StorNVMe SCSI 转换支持
description: StorNVMe SCSI 转换支持
ms.assetid: cd903ef8-9528-46a5-a276-06cf2fff2b88
ms.date: 01/13/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3ba918b2dc76b2a99c8d095f194f36b6f91c08cb
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706928"
---
# <a name="stornvme-scsi-translation-support"></a>StorNVMe SCSI 转换支持

下表列出了 SCSI 命令和已转换的 NVMe 命令（如果适用）。 Windows 10 版本1903及更高版本上的**StorNVMe**符合 SCSI 转换参考修订版1.5。

| SCSI 命令 | NVMe 命令 |
| ------------ | ------------ |
| 格式化单元/净化    | 格式 NVM                  |
| 查询                 | 身份                    |
| 日志感知               | 获取功能，获取日志页  |
| 模式选择（10）        | -                           |
| 模式感应（10）         | 确定、获取功能      |
| 读取（10）               | 已阅读                        |
| Read （16）               | 已阅读                        |
| 读取容量（10）      | 身份                    |
| 读取容量（16）      | 身份                    |
| 读取数据缓冲区16     | 获取日志页                |
| 报表 Lun             | 身份                    |
| 安全协议    | 安全接收            |
| 安全协议外   | 安全发送               |
| 发送诊断         | 不适用                         |
| 开始停止单元         | 设置功能，获取功能  |
| 同步缓存（10）  | 刷新                       |
| 测试单元准备就绪         | -                           |
| Unmap                   | 数据集管理          |
| 验证10               | 验证                      |
| 验证16               | 验证                      |
| 写入10                | 写入                       |
| 写入16                | 写入                       |
| 写入缓冲区            | 固件下载，激活 |
