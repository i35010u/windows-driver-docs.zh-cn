---
title: 视频微型端口驱动程序中的中断
description: 视频微型端口驱动程序中的中断
ms.assetid: bf84a3fb-860a-4647-ac34-93f3a22b166b
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，中断
- 中断 WDK 视频微型端口
- HwVidInterrupt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc50c73094b3c9ee6daa6cb0166bcdd996617792
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840353"
---
# <a name="interrupts-in-video-miniport-drivers"></a>视频微型端口驱动程序中的中断


## <span id="ddk_interrupts_in_video_miniport_drivers_gg"></span><span id="DDK_INTERRUPTS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


用于生成中断的适配器的视频微型端口驱动程序必须实现[*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)例程。 微型端口驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)例程应将视频的**HwInterrupt**成员初始化[ **\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)结构指向中断处理程序。

如果适配器生成中断，视频端口驱动程序会为视频微型端口驱动程序设置中断对象。 由于中断对象由视频端口驱动程序创建和管理，因此视频微型端口驱动程序编写器不需要有关中断对象的其他信息。

如果微型端口驱动程序的[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)函数发现视频适配器实际上不会生成中断，或者无法确定适配器的有效中断矢量/级别，则*HwVidFindAdapter*应同时设置这两个视频中的 InterruptLevel 和**INTERRUPTVECTOR** [ **\_端口\_CONFIG\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_port_config_info)结构到零。

当*HwVidFindAdapter*返回 control 时，视频端口驱动程序会检查\_视频中的中断配置成员\_CONFIG\_信息，如果两者均为零，则不会连接微型端口驱动程序的中断。 在*HwVidFindAdapter*中将这两个中断配置成员显式设置为0会禁用微型端口驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/display/driverentry-of-video-miniport-driver)函数设置的[*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)入口点（如果有）。

请注意， *HwVidInterrupt*可以访问微型端口驱动程序的设备扩展，因为它未分页。 根据微型端口驱动程序的设计，其他驱动程序函数可能不可能使用*HwVidInterrupt*安全地共享设备扩展或设备扩展的特定区域。

例如，假设微型端口驱动程序的[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数在适配器中断时访问设备扩展， *HwVidInterrupt*在另一个处理器上运行， *HwVidInterrupt*还访问设备扩展。 如果可能出现这种情况， *HwVidStartIO*应使用驱动程序提供的[*HwVidSynchronizeExecutionCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_synchronize_routine)函数调用[**VideoPortSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsynchronizeexecution) 。

视频微型端口驱动程序应遵循以下两个规则：

1.  只要微型端口驱动程序和硬件处于 D0 以外的任何状态，硬件就*不会*产生中断。

2.  由于规则1，如果电源状态为 D3 （应返回**FALSE**），则设备驱动程序 ISR*绝不*应在中断上操作。

 

 





