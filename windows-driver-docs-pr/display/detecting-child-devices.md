---
title: 检测子设备
description: 检测子设备
ms.assetid: 36c0c4ef-7810-4e8a-b349-0b7c1f8c2f0c
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，子设备
- 子设备 WDK 微型端口，检测
- 检测子设备 WDK 微型端口
- HwVidGetVideoChildDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2ea7678a3883d317618a2ee416da83f6a93f0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384880"
---
# <a name="detecting-child-devices"></a>检测子设备


## <span id="ddk_detecting_child_devices_gg"></span><span id="DDK_DETECTING_CHILD_DEVICES_GG"></span>


必须实现[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)插管理器能够检测到的图形适配器的子设备微型端口驱动程序中。

默认情况下[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)后父设备是否已启动; 不能调用之前，即*HwVidGetVideoChildDescriptor*不能调用直到后[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)已完成。 若要替代此默认设置，从而允许子枚举发生在任何时候，可以设置**AllowEarlyEnumeration**的成员[**视频\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)到**TRUE**。

当新的硬件连接到系统或现有的硬件系统断开连接时，某些设备生成中断。 若要处理此类中断，微型端口驱动程序应执行以下操作：

-   实现 DPC ([**HwVidDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_dpc_routine)) 来调用[ **VideoPortEnumerateChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportenumeratechildren)。

-   实现一个中断处理程序 ([*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)) 来调用[ **VideoPortQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueuedpc)进行排队时在中断 DPC设备会发生。

[**VideoPortEnumerateChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportenumeratechildren)微型端口驱动程序，从而强制的适配器的子设备重新枚举[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)函数若要调用的每个父设备的子级。 插管理器将相应地更新父设备与其子项之间的关系。

 

 





