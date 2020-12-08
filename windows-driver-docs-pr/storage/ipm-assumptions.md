---
title: 空闲电源管理假设
description: 空闲电源管理假设
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e06e8671e23f1736de35aebb32806011b3bbd37
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804455"
---
# <a name="idle-power-management-assumptions"></a>空闲电源管理假设

磁盘启动操作在240秒内完成， (4 分钟后) 从将 SCSI 启动单元命令发出到 LUN 的时间。

以下 SCSI 命令 (需要完成 SRB_FUNCTION_EXECUTE_SCSI 操作) ，而无需启动磁盘。 换言之，无需执行前面的 SCSI 启动单元命令。

- 查询

- 报表 LUN

小型端口驱动程序应在 LUN 处于低功耗状态时完成所有 SRBs （SRB_FUNCTION_IO_CONTROL、SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN 除外）。
