---
title: 视频微型端口驱动程序中的中断
description: 视频微型端口驱动程序中的中断
ms.assetid: bf84a3fb-860a-4647-ac34-93f3a22b166b
keywords:
- 微型端口驱动程序 WDK Windows 2000，中断
- 中断 WDK 微型端口
- HwVidInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fb0d6c8b56c7a984c76541c2b006ebd3527f142
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379900"
---
# <a name="interrupts-in-video-miniport-drivers"></a>视频微型端口驱动程序中的中断


## <span id="ddk_interrupts_in_video_miniport_drivers_gg"></span><span id="DDK_INTERRUPTS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


用于生成中断的适配器的微型端口驱动程序必须实现[ *HwVidInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)例程。 微型端口驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)例程应初始化**HwInterrupt**隶属[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)结构，以指向中断处理程序。

视频端口驱动程序设置的微型端口驱动程序的中断对象，如果适配器生成中断。 创建并管理的视频端口驱动程序中断对象，因为微型端口驱动程序编写器需要中断对象的任何进一步信息。

如果微型端口驱动程序[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)函数查找视频适配器不会实际生成中断或无法确定向量/级别对于适配器，有效中断*HwVidFindAdapter*应同时设置**InterruptLevel**并**InterruptVector**中[**视频\_端口\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_port_config_info)为零的结构。

当*HwVidFindAdapter*返回控件中，视频端口驱动程序将查看在视频中的中断配置成员\_端口\_配置\_信息和，如果二者都为零，不会连接中断微型端口驱动程序。 显式将两者都设置中断配置成员将注意力集中在*HwVidFindAdapter*禁用[ *HwVidInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)入口点，如果有，通过设置微型端口驱动程序[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)函数。

请注意， *HwVidInterrupt*可以访问微型端口驱动程序的设备扩展，因为它是未分页。 根据微型端口驱动程序的设计，它可能不是通过共享设备扩展或与设备扩展的特定区域的其他驱动程序函数*HwVidInterrupt*安全。

例如，假设微型端口驱动程序[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)函数时，适配器会中断，访问设备扩展*HwVidInterrupt*上运行另一个处理器，并*HwVidInterrupt*还可访问设备扩展。 如果可能发生这种情况，则*HwVidStartIO*应调用[ **VideoPortSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportsynchronizeexecution)与驱动程序提供[ *HwVidSynchronizeExecutionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_synchronize_routine)函数。

微型端口驱动程序应遵循以下两个规则：

1.  每当微型端口驱动程序和硬件处于任何状态以外 D0，硬件*永远不会*生成中断。

2.  由于规则 1 中，应将设备驱动程序 ISR*永远不会*D3 的电源状态是否处理中断 (它应返回**FALSE**)。

 

 





