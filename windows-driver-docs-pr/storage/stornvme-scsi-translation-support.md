---
title: StorNVMe SCSI 转换支持
description: StorNVMe SCSI 转换支持
ms.date: 05/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 392437955a44a5b82d4d489d34f0db188ef7b614
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834951"
---
# <a name="stornvme-scsi-translation-support"></a>StorNVMe SCSI 转换支持

下表列出了 SCSI 命令和已转换的 NVMe 命令 (s) （如果适用）。 Windows 10 版本1903及更高版本上的 **StorNVMe** 符合 SCSI 转换参考修订版1.5。

有关其他信息，请参阅使用 [NVMe 驱动器](/windows/win32/fileio/working-with-nvme-devices#protocol-specific-queries) 。

| SCSI 命令 | NVMe 命令 |
| ------------ | ------------ |
| 格式化单元/净化    | 格式 NVM                  |
| 查询                 | 识别                    |
| 日志感知               | 获取功能，获取日志页  |
| 模式选择 (10)         | -                           |
| Mode Sense (10)          | 确定、获取功能      |
| 读取 (10)                | 读取                        |
| 读取 (16)                | 读取                        |
| 读取容量 (10)       | 识别                    |
| 读取容量 (16)       | 识别                    |
| 读取数据缓冲区16     | 获取日志页                |
| 报表 Lun             | 识别                    |
| 安全协议    | 安全接收            |
| 安全协议外   | 安全发送               |
| 发送诊断         | 不适用                         |
| 开始停止单元         | 设置功能，获取功能  |
| 同步缓存 (10)   | 刷新                       |
| 测试单元准备就绪         | -                           |
| Unmap                   | 数据集管理          |
| 验证10               | Verify                      |
| 验证16               | Verify                      |
| 写入10                | 写入                       |
| 写入16                | 写入                       |
| 写入缓冲区            | 固件下载，激活 |
