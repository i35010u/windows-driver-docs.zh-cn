---
title: 更改用于调试的 GPU 计划程序的行为
description: 更改用于调试的 GPU 计划程序的行为
keywords:
- GPU 计划程序更改 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50d1ffb6b04525a53eacb14a1df6be3d27dbdecf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810325"
---
# <a name="changing-the-behavior-of-the-gpu-scheduler-for-debugging"></a>更改用于调试的 GPU 计划程序的行为


为了帮助调试驱动程序，可以通过配置注册表更改图形处理单元 (GPU) 计划程序的行为。

可以通过 GPU 计划程序启用或禁用抢占请求 (参阅 [超时检测和恢复](timeout-detection-and-recovery.md)) 使用以下注册表配置：

```registry
KeyPath   : HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Scheduler
KeyValue  : EnablePreemption
ValueType : REG_DWORD
ValueData : 0 to disable preemption, 1 to enable preemption (default).
```

 

 





