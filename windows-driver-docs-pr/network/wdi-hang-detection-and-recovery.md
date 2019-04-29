---
title: 挂起检测和恢复
description: 命令发出到 IHV 组件后，主机将启动一个计时器。
ms.assetid: 89133252-C08C-4ADC-A5EE-E46A91909337
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbce550fe7744e921d732085f37a0a7abe5fcaa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367527"
---
# <a name="hang-detection-and-recovery"></a>挂起检测和恢复


命令发出到 IHV 组件后，主机将启动一个计时器。 如果在计时器过期之前 IHV 组件完成 (步骤 3 的图中的消息[通信模型、 同步和中止](wdi-communication-model.md))，驱动程序假定 IHV 组件已挂起、 重置 IHV 组件，并恢复如果不满足前提条件是正确的。

不满足前提条件是，系统将提供 ACPI 方法重置设备，在总线或在设备级别。

M1 M3 的挂起超时值为 10 秒。

M3 M4 任务挂起超时为 30 秒，或可配置基于任务。

> [!NOTE]
> 某些任务可能需要花费的时间超过 30 秒才能完成 （例如，Wi-Fi Direct 发现在某些方案中的所选的注册机构位）。 在这些情况下，主机启动的任务超时是相应地调整为 30 秒，超过该任务的最大预期的运行时允许。 

这些是为命令的最大上限并处理所花时间超过此时间被视为错误。 应该就是，在操作 （无 CPU 压力） 正常模式下，大多数任务和属性完成显著低于上面指定的超时。 与每个任务/属性指定这些值。 适配器应确保它不具有将导致超过这些执行时间的等待。

## <a name="in-this-section"></a>本节内容

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md)
[UE 挂起检测： 步骤 1-14](wdi-ue-hang-detection--step-1-to-step-14.md)
[重置 （意外删除）： 步骤 15 到 20](wdi-reset--surprise-remove---steps-15-20.md) 
 [诊断调用的计时](wdi-timings-for-diagnose-call.md)
[LE 挂起检测](wdi-le-hang-detection.md)
[PLDR](wdi-pldr-and-fldr.md)
 

 





