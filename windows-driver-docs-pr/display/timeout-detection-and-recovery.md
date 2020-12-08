---
title: 超时检测和恢复 (TDR)
description: '描述 Windows 显示驱动程序模型 (WDDM) 的超时检测和恢复 (TDR) '
keywords:
- TDR (超时检测和恢复) WDK 显示
- TDR (超时检测和恢复) WDK 图形
ms.date: 10/06/2020
ms.localizationpriority: medium
ms.custom: contperfq2
ms.openlocfilehash: 90a4e0581a1cd6f527bf9bfad4df792b0344035f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821513"
---
# <a name="timeout-detection-and-recovery-tdr"></a>超时检测和恢复 (TDR)

本页介绍了驱动程序开发人员 (TDR) 的超时检测和恢复。 另请参阅 [Windows 8 及更高版本中的 TDR](tdr-changes-in-windows-8.md) ，以获取其他实现详细信息。

## <a name="overview"></a>概述

当计算机 "挂起" 时，或者在实际情况下，它是在处理最终用户命令或操作时，图形中最常见的稳定性问题之一。 用户通常会等待几秒钟，然后决定重新启动计算机。 通常会发生计算机的冻结外观，因为 GPU 在游戏播放期间通常忙于处理密集型图形操作，因此不会更新显示屏幕。 Tdr 使操作系统能够检测 UI 没有响应。

下图显示了 TDR 进程。

![超时检测和恢复 (通过 wddm 进行的 gpu) tdr](images/timeoutdetectionrecoverygpusthroughwddm.jpg)

操作系统 (操作系统) 尝试检测计算机看似 "冻结" 的情况。 然后，操作系统会尝试在冻结的情况下动态恢复，使桌面再次响应，从而减轻最终用户不必要地重新启动其系统的情况。

如果操作系统检测到六个 (6) 或多个 GPU 挂起，并且后续恢复在一 (1) 分钟内发生，则操作系统 bug-将在下一个 GPU 挂起时检查计算机。

## <a name="timeout-detection-in-wddm"></a>WDDM 中的超时检测

GPU 计划程序是 (*Dxgkrnl.sys*) 的 DirectX graphics 内核子系统的一部分，它检测到 GPU 所用的时间超过了所允许的执行特定任务的时间量。 然后，GPU 计划程序将尝试抢占此特定任务。 Preempt 操作具有 "等待" 超时，这是实际的 TDR 超时。 Windows Vista 和更高版本操作系统中的默认超时时间为2秒。 如果 GPU 无法在 TDR 超时期限内完成或抢占当前任务，操作系统会诊断 GPU 已冻结。

为了防止发生超时检测，硬件供应商应确保图形操作 (也就是说， (DMA) 缓冲器完成的直接内存访问) 在工作效率和游戏播放等最终用户方案中不超过2秒。

## <a name="preparation-for-recovery"></a>恢复准备

GPU 计划程序将调用显示微型端口驱动程序的 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数，以通知驱动程序操作系统检测到超时。 然后，驱动程序必须重新初始化自身并重置 GPU。 此外，驱动程序必须停止访问内存，并且不应访问硬件。 操作系统和驱动程序收集硬件和其他状态信息，这些信息可用于恢复后诊断。

有关其他实现的详细信息，请参阅 [Windows 8 及更高版本中的 TDR](tdr-changes-in-windows-8.md) 。

## <a name="desktop-recovery"></a>桌面恢复

OS 将重置图形堆栈的适当状态。 视频内存管理器也是 *Dxgkrnl.sys* 的一部分，它将清除视频内存中的所有分配。 显示微型端口驱动程序会重置 GPU 硬件状态。 图形堆栈会执行最后的操作，并将桌面还原为响应状态。

从挂起检测到恢复的唯一可见项目是屏幕闪烁。 当 OS 重置图形堆栈的某些部分（这会导致屏幕重绘）时，会出现此闪烁。 如果显示微型端口驱动程序符合 WDDM 1.2 和更高版本，则会将其排除 (请参阅 [在 WDDM 1.2 和更高) 版本中提供无缝状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md) 。

当操作系统成功恢复桌面时，它将执行以下操作：

* 向最终用户显示一条信息性消息，指出 "显示驱动程序已停止响应并已恢复"。
* 在事件查看器应用程序中记录前面的消息，并以调试报表的形式收集诊断信息。 如果最终用户选择提供反馈，则 OS 会通过联机故障分析将此调试报告返回给 Microsoft， (OCA) 机制。

某些旧的 DirectX 应用程序可能只在此恢复结束时呈现黑色，这需要最终用户重新启动这些应用程序。 妥善编写的 DirectX 9Ex 和 DirectX 10 及更高版本的应用程序可继续正常工作。 应用程序必须发布，然后重新创建其 Microsoft Direct3D 设备和所有设备的对象。

## <a name="thread-synchronization-and-tdr"></a>线程同步和 TDR

有关详细信息，请参阅 [线程同步和 TDR](thread-synchronization-and-tdr.md) 。

## <a name="testing-and-debugging-tdr"></a>测试和调试 TDR

有关详细信息，请参阅 [测试和调试 TDR](tdr-registry-keys.md) 。
