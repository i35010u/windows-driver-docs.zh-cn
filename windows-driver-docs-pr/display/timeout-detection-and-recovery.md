---
title: '超时检测和恢复 (TDR) '
description: '超时检测和恢复 (TDR) '
ms.assetid: f410eec7-026f-41e0-8c60-72f651659ead
keywords:
- TDR (超时检测和恢复) WDK 显示，介绍
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a23cd794bf4254f4de083810d3fcb13088e45f3a
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063740"
---
# <a name="timeout-detection-and-recovery-tdr"></a>超时检测和恢复 (TDR) 


当计算机 "挂起" 或完全显示为 "已冻结" 时，图形中的最常见稳定性问题之一就是，实际上它正在处理最终用户的命令或操作。 最终用户通常会等待几秒钟，然后决定重新启动计算机。 通常会发生计算机的冻结外观，因为 GPU 在游戏播放期间通常忙于处理密集型图形操作。 GPU 不会更新显示屏幕，并且计算机会显示为冻结状态。

在 Windows Vista 和更高版本中，操作系统会尝试检测计算机看上去完全 "冻结" 的情况。 然后，操作系统会尝试在冻结的情况下动态恢复，以便桌面再次响应。 此检测和恢复过程称为 *超时检测和恢复* (TDR) 。 在 TDR 过程中，操作系统的 GPU 计划程序将调用显示微型端口驱动程序的 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数来重新初始化驱动程序并重置 GPU。 因此，最终用户不需要重新启动操作系统，这大大增强了其体验。

从挂起检测到恢复的唯一可见项目是屏幕闪烁。 当操作系统重置图形堆栈的某些部分（这会导致屏幕重绘）时，此屏幕会闪烁。 如果显示微型端口驱动程序符合 Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本，则会消除此闪烁 (请参阅 [在 WDDM 1.2 和更高) 版本中提供无缝状态转换](seamless-state-transitions-in-wddm-1-2-and-later.md) 。 某些旧的 Microsoft DirectX 应用程序 (例如，符合) 9.0 之前的 DirectX 版本的 DirectX 应用程序在此恢复结束时，可能会呈现为黑屏。 最终用户需要重新启动这些应用程序。

此顺序简要介绍了 TDR 过程：

## <a name="span-idtimeout_detection_in_the_windows_display_driver_model__wddm_spanspan-idtimeout_detection_in_the_windows_display_driver_model__wddm_spanspan-idtimeout_detection_in_the_windows_display_driver_model__wddm_spantimeout-detection-in-the-windows-display-driver-model-wddm"></a><span id="Timeout_detection_in_the_Windows_Display_Driver_Model__WDDM_"></span><span id="timeout_detection_in_the_windows_display_driver_model__wddm_"></span><span id="TIMEOUT_DETECTION_IN_THE_WINDOWS_DISPLAY_DRIVER_MODEL__WDDM_"></span>Windows 显示驱动程序模型中的超时检测 (WDDM) 


GPU 计划程序是 DirectX 图形内核子系统 ( # A0) 的一部分，它检测到 GPU 所用的时间超过了所允许的执行特定任务的时间量。 然后，GPU 计划程序将尝试抢占此特定任务。 Preempt 操作具有 "等待" 超时，这是实际的 TDR 超时。 因此，此步骤是进程的超时检测阶段。 Windows Vista 和更高版本操作系统中的默认超时时间为2秒。 如果 GPU 无法在 TDR 超时期限内完成或抢占当前任务，操作系统会诊断 GPU 已冻结。

为了防止发生超时检测，硬件供应商应确保图形操作 (也就是说， (DMA) 缓冲器完成的直接内存访问) 在工作效率和游戏播放等最终用户方案中不超过2秒。

## <a name="span-idpreparation_for_recoveryspanspan-idpreparation_for_recoveryspanspan-idpreparation_for_recoveryspanpreparation-for-recovery"></a><span id="Preparation_for_recovery"></span><span id="preparation_for_recovery"></span><span id="PREPARATION_FOR_RECOVERY"></span>恢复准备


操作系统的 GPU 计划程序调用显示微型端口驱动程序的 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数，以通知驱动程序操作系统检测到超时。 然后，驱动程序必须重新初始化自身并重置 GPU。 此外，驱动程序必须停止访问内存，并且不应访问硬件。 操作系统和驱动程序收集硬件和其他可能对事后诊断有用的状态信息。

## <a name="span-iddesktop_recoveryspanspan-iddesktop_recoveryspanspan-iddesktop_recoveryspandesktop-recovery"></a><span id="Desktop_recovery"></span><span id="desktop_recovery"></span><span id="DESKTOP_RECOVERY"></span>桌面恢复


操作系统重置图形堆栈的适当状态。 视频内存管理器也是 Dxgkrnl.sys 的一部分，它将清除视频内存中的所有分配。 显示微型端口驱动程序会重置 GPU 硬件状态。 图形堆栈会执行最后的操作，并将桌面还原为响应状态。 如前所述，某些旧的 DirectX 应用程序在此恢复结束时可能仅呈现为黑色，这需要最终用户重新启动这些应用程序。 妥善编写的 DirectX 9Ex 和 DirectX 10 及更高版本的应用程序可继续正常工作。 应用程序必须发布，然后重新创建其 Microsoft Direct3D 设备和所有设备的对象。 有关 DirectX 应用程序如何恢复的详细信息，请参阅 Windows SDK。

## <a name="span-idrelated_tdr_topicsspanspan-idrelated_tdr_topicsspanspan-idrelated_tdr_topicsspanrelated-tdr-topics"></a><span id="Related_TDR_topics"></span><span id="related_tdr_topics"></span><span id="RELATED_TDR_TOPICS"></span>相关 TDR 主题


以下主题介绍了启用 TDR 调试的 TDR 过程和注册表项：

[限制重复性 GPU 挂起和恢复](limiting-repetitive-gpu-hangs-and-recoveries.md)

[TDR 错误消息](tdr-error-messaging.md)

[TDR 注册表项](tdr-registry-keys.md)

[Windows 8 中的 TDR 更改](tdr-changes-in-windows-8.md)

 

