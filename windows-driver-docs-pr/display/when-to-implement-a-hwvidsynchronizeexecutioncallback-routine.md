---
title: 实现 HwVidSynchronizeExecutionCallback 例程
description: 何时实现 HwVidSynchronizeExecutionCallback 例程
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，中断
- 中断 WDK 视频微型端口
- HwVidSynchronizeExecutionCallback
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: df79bd533492517f7d4b8171b5e03dcace4bcdd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826029"
---
# <a name="implementing-a-hwvidsynchronizeexecutioncallback-routine"></a>实现 HwVidSynchronizeExecutionCallback 例程

不产生中断的适配器的微型端口驱动程序很少使用 [*HwVidSynchronizeExecutionCallback*](/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)函数调用 [**VideoPortSynchronizeExecution**](/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution) 。

事实上，即使是具有 [*HwVidInterrupt*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt) 函数的小型小型驱动程序也不一定具有 *HwVidSynchronizeExecutionCallback* 函数。 由于视频端口驱动程序在处理完前面的请求之前，不会向微型端口驱动程序的 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io) 函数发送请求 (请参阅 [ (Windows 2000 模型处理视频请求)](processing-video-requests--windows-2000-model-.md) 有关详细信息) ，微型端口驱动程序很少调用 **VideoPortSynchronizeExecution**。

微型端口驱动程序的 *HwVidSynchronizeExecutionCallback* 函数有两种可能的用法：

-   若要使用 *HwVidInterrupt* 函数之外的驱动程序函数访问适配器，请使用微型端口驱动程序的设备扩展。

    向 *HwVidSynchronizeExecutionCallback* 函数提供控制后，适配器的中断会被屏蔽，因此当 *HWVIDSYNCHRONIZEEXECUTIONCALLBACK* 函数在 SMP 计算机中运行时，微型端口驱动程序的 *HwVidInterrupt* 函数无法更改设备扩展中的状态。

-   如果适配器需要，将命令快速写入适配器注册或端口。

    如果为 *HwVidSynchronizeExecutionCallback* 函数提供了控制，几乎所有系统中断都将被屏蔽，因此 *HwVidSynchronizeExecutionCallback* 函数不能被设备占用 (甚至) 中断。

    *HwVidSynchronizeExecutionCallback* 函数 *必须* 尽快返回 control。

对于第一种类型的 [*HwVidSynchronizeExecutionCallback*](/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine) 函数，微型端口驱动程序将调用 [**VideoPortSynchronizeExecution**](/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution) ，并将 *优先级* 设置为 **VpMediumPriority**。 对于第二种类型 *的 HwVidSynchronizeExecutionCallback* 函数，如果驱动程序没有 [*HwVidInterrupt*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)函数，则微型端口驱动程序还会将 *优先级* 设置为 **VpMediumPriority** 。 否则，此类微型端口驱动程序会将 *优先级* 设置为 **VpHighPriority** 进行此调用。

通常情况下，微型端口驱动程序 *不* 应使用第二种类型的 *HwVidSynchronizeExecutionCallback* 函数调用 **VideoPortSynchronizeExecution** ，除非驱动程序设计器没有其他替代项：也就是说，除非该适配器必须在系统中断被屏蔽的情况下进行编程。 否则，微型端口驱动程序应调用 **VideoPortSynchronizeExecution** ，并将 *优先级* 设置为 **VpLowPriority**。

*HwVidSynchronizeExecutionCallback* 函数（如 *HwVidInterrupt* 函数）无法分页，并且在不关闭系统的情况下无法调用某些 **VideoPort**_Xxx_ 函数。 有关 *HwVidSynchronizeExecutionCallback* 函数可安全调用的 **VideoPort**_Xxx_ 函数的摘要，请参阅 [*HwVidInterrupt*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)。

 

