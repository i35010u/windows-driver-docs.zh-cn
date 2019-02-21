---
title: 更改用于调试 GPU 计划程序的行为
description: 更改用于调试 GPU 计划程序的行为
ms.assetid: 72eef7bf-b775-4e02-acc6-b745a41c616a
keywords:
- GPU 计划程序更改 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f27e02aeb61026ed4cf029dc42c6cac63abfe389
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555470"
---
# <a name="changing-the-behavior-of-the-gpu-scheduler-for-debugging"></a>更改用于调试 GPU 计划程序的行为


为了帮助进行调试驱动程序，可以通过配置注册表更改的图形处理单元 (GPU) 计划程序的行为。

可以启用或禁用从 GPU 计划程序抢占请求 (请参阅[超时检测和恢复](timeout-detection-and-recovery.md)) 通过使用下面的注册表配置：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler
KeyValue  : EnablePreemption
ValueType : REG_DWORD
ValueData : 0 to disable preemption, 1 to enable preemption (default).
```

 

 





