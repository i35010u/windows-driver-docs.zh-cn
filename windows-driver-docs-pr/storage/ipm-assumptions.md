---
title: 空闲电源管理假设
description: 空闲电源管理假设
ms.assetid: 3c8d8121-9987-43d3-b573-4ca1d26fef7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0a519cdaccb34e5866d8edfe6c51a1246fb2e9d
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606378"
---
# <a name="idle-power-management-assumptions"></a>空闲电源管理假设

从向 LUN 发出 SCSI Start Unit 命令后，磁盘启动操作在240秒（4分钟）内完成。

以下 SCSI 命令（SRB_FUNCTION_EXECUTE_SCSI 操作）应在无需启动磁盘的情况下完成。 换言之，无需执行前面的 SCSI 启动单元命令。

- 查询

- 报表 LUN

小型端口驱动程序应在 LUN 处于低功耗状态时完成所有 SRBs （SRB_FUNCTION_IO_CONTROL、SRB_FUNCTION_FLUSH 和 SRB_FUNCTION_SHUTDOWN 除外）。
