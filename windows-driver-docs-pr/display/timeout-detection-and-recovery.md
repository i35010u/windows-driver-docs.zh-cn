---
title: 超时检测和恢复 (TDR)
description: 超时检测和恢复 (TDR)
ms.assetid: f410eec7-026f-41e0-8c60-72f651659ead
keywords:
- （超时检测和恢复） TDR WDK 显示，所述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1403613d73e985b5aef68d624cb38f203f593f1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566018"
---
# <a name="timeout-detection-and-recovery-tdr"></a>超时检测和恢复 (TDR)


一台计算机"挂起"或显示完全"冻结"，但实际上，它还处理最终用户的命令或操作时出现一个图形中最常见的稳定性问题。 最终用户通常在等待几秒钟，然后决定要重新启动计算机。 因为 GPU 正忙于处理密集的图形操作，通常在玩游戏期间，通常会发生冻结的计算机的外观。 GPU 不会更新显示屏幕上，并且计算机将出现冻结。

在 Windows Vista 及更高版本，操作系统将尝试检测计算机似乎完全"冻结"的情况。 操作系统然后尝试从已冻结的情况下动态恢复，以便桌面是再次响应。 此检测和恢复的过程称为*超时检测和恢复*(TDR)。 在 TDR 过程中，操作系统的 GPU 计划程序调用显示微型端口驱动程序[ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)函数以重新初始化该驱动程序和重置 GPU。 因此，最终用户不需要重新启动操作系统，极大地增强了他们的体验。

从挂起检测到恢复的唯一可见项目是屏幕闪烁。 当操作系统重置图形堆栈，这会导致屏幕重绘的某些部分时，此屏幕闪烁的结果。 如果显示微型端口驱动程序遵循与 Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本消除了此闪烁 (请参阅[提供无缝的状态转换 WDDM 1.2 及更高版本](seamless-state-transitions-in-wddm-1-2-and-later.md))。 此恢复结束时显示黑色屏幕可能会使某些旧版 Microsoft DirectX 应用程序 （例如，早于 9.0 符合 DirectX 版本的 DirectX 应用）。 最终用户将必须重新启动这些应用程序。

此序列简要介绍 TDR 过程：

## <a name="span-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspanspan-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspanspan-idtimeoutdetectioninthewindowsdisplaydrivermodelwddmspantimeout-detection-in-the-windows-display-driver-model-wddm"></a><span id="Timeout_detection_in_the_Windows_Display_Driver_Model__WDDM_"></span><span id="timeout_detection_in_the_windows_display_driver_model__wddm_"></span><span id="TIMEOUT_DETECTION_IN_THE_WINDOWS_DISPLAY_DRIVER_MODEL__WDDM_"></span>超时检测在 Windows 显示驱动程序模型 (WDDM)


GPU 计划程序，它是 DirectX 图形内核子系统 (Dxgkrnl.sys) 的一部分，检测到 GPU 花费超过允许的时间来执行特定任务的详细信息。 GPU 计划程序然后尝试抢占这一特定任务。 Preempt 操作具有"等待"超时，这是实际 TDR 超时。 因此，此步骤是过程的超时检测阶段。 在 Windows Vista 和更高版本操作系统的默认超时时间为 2 秒。 如果 GPU 无法完成，或在 TDR 超时期限内抢占当前任务，操作系统将诊断 GPU 已被冻结。

若要防止发生超时检测，硬件供应商应确保图形操作 （即，直接内存访问 (DMA) 缓冲区完成），需要在最终用户工作效率和玩游戏等方案中不能超过 2 秒。

## <a name="span-idpreparationforrecoveryspanspan-idpreparationforrecoveryspanspan-idpreparationforrecoveryspanpreparation-for-recovery"></a><span id="Preparation_for_recovery"></span><span id="preparation_for_recovery"></span><span id="PREPARATION_FOR_RECOVERY"></span>恢复的做准备


操作系统的 GPU 计划程序调用显示微型端口驱动程序[ *DxgkDdiResetFromTimeout* ](https://msdn.microsoft.com/library/windows/hardware/ff559815)函数来通知该驱动程序，操作系统检测到了超时。 该驱动程序必须重新初始化自身，然后重置 GPU。 此外，驱动程序必须停止访问内存，并且不应访问硬件。 操作系统和驱动程序，收集硬件和可能适用于事后诊断其他状态信息。

## <a name="span-iddesktoprecoveryspanspan-iddesktoprecoveryspanspan-iddesktoprecoveryspandesktop-recovery"></a><span id="Desktop_recovery"></span><span id="desktop_recovery"></span><span id="DESKTOP_RECOVERY"></span>桌面恢复


操作系统重置图形堆栈的适当的状态。 视频内存管理器，也是 Dxgkrnl.sys 的一部分，将清除所有从视频内存分配。 显示微型端口驱动程序将重置 GPU 硬件状态。 图形堆栈执行的最后一个操作，并将在桌面上还原到响应的状态。 如前文所述，某些旧版 DirectX 应用程序可能会使此恢复，这需要最终用户在重新启动这些应用程序结束时只是黑色。 编写良好的 DirectX 9Ex 和 DirectX 10 和更高版本的应用程序处理设备中删除技术仍正常工作。 应用程序必须发布，然后重新创建其 Microsoft Direct3D 设备和所有设备的对象。 有关如何恢复 DirectX 应用程序的详细信息，请参阅 Windows SDK。

## <a name="span-idrelatedtdrtopicsspanspan-idrelatedtdrtopicsspanspan-idrelatedtdrtopicsspanrelated-tdr-topics"></a><span id="Related_TDR_topics"></span><span id="related_tdr_topics"></span><span id="RELATED_TDR_TOPICS"></span>相关的 TDR 主题


这些主题中介绍了 TDR 和注册表项启用 TDR 调试：

[限制重复 GPU 挂起和恢复](limiting-repetitive-gpu-hangs-and-recoveries.md)

[TDR 错误消息传送](tdr-error-messaging.md)

[TDR 注册表项](tdr-registry-keys.md)

[在 Windows 8 中 TDR 更改](tdr-changes-in-windows-8.md)

 

 





