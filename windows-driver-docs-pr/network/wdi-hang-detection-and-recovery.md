---
title: 挂起检测和恢复
description: 将命令发送到 IHV 组件后，主机会启动计时器。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48e419cc98ff99f756c241d42327c38b5d3871b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836271"
---
# <a name="hang-detection-and-recovery"></a>挂起检测和恢复


将命令发送到 IHV 组件后，主机会启动计时器。 如果在 " [通信模型"、"同步" 和 "中止](wdi-communication-model.md) ") 中的 " (第3步" 消息完成后，计时器过期，则驱动程序会假设 ihv 组件已挂起、重置 ihv 组件，并在前提条件正确时恢复。

前提条件是，系统将提供 ACPI 方法，以便在总线或设备级别重置设备。

M1-M3 挂起超时值为10秒。

M3-M4 任务挂起超时为30秒，或可根据任务进行配置。

> [!NOTE]
> 某些任务可能需要超过30秒的时间才能完成 (例如，在某些情况下 Wi-Fi 直接发现所选注册位) 。 在这些情况下，将相应地调整主机启动的任务超时值，以允许比预期的最大运行时任务长30秒。 

这些是命令和处理时间超过此时间的最大上限被视为错误。 预期在正常运行模式下 (不) CPU 压力，大多数任务和属性的完成时间远远早于以上指定的超时时间。 这些值是通过每个任务/属性指定的。 适配器应确保它不会导致超出执行时间的等待。

## <a name="in-this-section"></a>在本节中

[UE 挂起检测和恢复流](wdi-ue-hang-detection-and-recovery-flow.md) 
[UE 挂起检测：步骤 1-14](wdi-ue-hang-detection--step-1-to-step-14.md) 
[重置 (意外删除) ：步骤 15-20](wdi-reset--surprise-remove---steps-15-20.md) 
[诊断呼叫](wdi-timings-for-diagnose-call.md) 
 的计时[LE 挂起检测](wdi-le-hang-detection.md) 
[PLDR](wdi-pldr-and-fldr.md)
 

 





