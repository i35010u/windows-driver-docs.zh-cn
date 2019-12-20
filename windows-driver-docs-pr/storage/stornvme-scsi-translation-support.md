---
title: StorNVMe SCSI 转换支持
description: StorNVMe SCSI 转换支持
ms.assetid: cd903ef8-9528-46a5-a276-06cf2fff2b88
ms.date: 12/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9bdbee9cd952cf7a67bfeb379b4942f031d9586b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252076"
---
# <a name="stornvme-scsi-translation-support"></a>StorNVMe SCSI 转换支持

下表列出了 SCSI 命令和已转换的 NVMe 命令（如果适用）。 **StorNVMe**符合 SCSI 转换参考修订版1.5。

| SCSI 命令 | NVMe 命令 | 备注 |
| ------------ | ------------ | -------- |
| 比较和写入 *      | 比较和写入           |
| 格式化单元/净化    | 格式 NVM                  |
| 查询                 | 指出                    |
| 日志感知               | 获取功能，获取日志页  |
| 模式选择（6） *        | -                           |
| 模式选择（10）        | -                           |
| 模式感知（6） *         | 确定、获取功能      |
| 模式感应（10）         | 确定、获取功能      |
| Read （6） *               | 已阅读                        |
| 读取（10）               | 已阅读                        |
| Read （12） *              | 已阅读                        |
| Read （16）               | 已阅读                        |
| 读取容量（10）      | 指出                    |
| 读取容量（16）      | 指出                    |
| 读取数据缓冲区16     | 获取日志页                |
| 报表 Lun             | 指出                    |
| 请求意义 *          | -                           |
| 安全协议    | 安全接收            |
| 安全协议外   | 安全发送               |
| 发送诊断         | 不适用                         |
| 开始停止单元         | 设置功能，获取功能  |
| 同步缓存（10）  | 刷新                       |
| 同步缓存（16） * | 刷新                       |
| 测试单元准备就绪         | -                           |
| Unmap                   | 数据集管理          |
| 验证10               | 验证                      |
| 验证 12 *              | 验证                      |
| 验证16               | 验证                      |
| 写入长 10 *          | 写入无法纠正         |
| 写入 Long 16 *          | 写入无法纠正         |
| 写入 6 *                | 写入                       |
| 写入10                | 写入                       |
| 写入 12 *               | 写入                       |
| 写入16                | 写入                       |
| 写入缓冲区            | 固件下载，激活 |

*使用星号 \* SCSI 命令包含可翻译的 NVMe 命令; 但是， *StorNVMe*当前不支持此转换。*
