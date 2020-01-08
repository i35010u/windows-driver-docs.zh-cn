---
title: 空闲电源管理硬盘驱动器空闲超时
description: 空闲电源管理硬盘驱动器空闲超时
ms.assetid: 1dcc261a-803c-4c0e-a68e-29b00f46cd32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 966d4b16bc415f731f9f7d89bca0753e38b72cc3
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606543"
---
# <a name="idle-power-management-hard-disk-drive-idle-timeout"></a>空闲电源管理硬盘驱动器空闲超时

尽管硬盘（HDD）不是典型移动 PC 中的主要电源使用者，但通过旋转 HDD 介质可以实现节能。 "HDD 空闲超时" 允许 Windows 在一段时间内磁盘读取和写入不活动后自动降速 HDD 媒体。

在 HDD 介质旋转时实现的节能方式因 HDD 的品牌和型号而异。 我们鼓励系统制造商与 HDD 供应商合作，以确定特定设备的最佳 HDD 空闲超时值。

默认情况下，Windows Vista 指定适度的硬盘驱动器空闲超时值。 如果在移动 Pc 上尝试实现高电量节约，系统制造商应考虑指定较短的值。 下表汇总了 HDD 空闲设置的详细信息。

| 详情 | 描述 |
| ------ | ----------- |
| 友好名称     | 后关闭硬盘 |
| 描述       | 指定在磁盘关闭前硬盘驱动器处于非活动状态的时长 |
| PowerCfg 别名    | DISKIDLE |
| 组策略路径 | 管理 Templates\System\Power Management\Hard Disk Settings\Turn 硬盘 |
| GUID              | 6738e2c4-e8a5-4a42-b16a-e040e769756e |
| 定义位置        | Ntpoapi |
| 平衡默认值 | 60分钟（AC）30分钟（DC） |

有关详细信息，请参阅[移动电池使用方案-适用于移动平台专业人员的指南。](https://go.microsoft.com/fwlink/p/?linkid=144534)
