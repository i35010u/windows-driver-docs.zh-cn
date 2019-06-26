---
title: 与子设备的驱动程序通信
description: 与子设备的驱动程序通信
ms.assetid: f1311941-bfba-44a4-867c-95fcbef19510
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，子设备
- 子设备 WDK 微型端口，与该驱动程序进行通信
- HwVidQueryInterface
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1d01f6495a3b87998805b3dacac26354c290c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370655"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>与子设备的驱动程序通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


微型端口驱动程序和子设备的驱动程序可以相互定义使子驱动程序与父微型端口驱动程序通过其硬件进行通信的接口。 子驱动程序将获取此接口通过发送[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)父微型端口驱动程序的视频端口驱动程序的请求。 视频端口驱动程序收到此类请求后，调用微型端口驱动程序[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)函数，如果定义，并微型端口驱动程序返回对接口的指针。 然后，子设备的驱动程序可以调用到通过公开的函数的微型端口驱动程序*HwVidQueryInterface*在任何时间。

如果微型端口驱动程序不实现[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)或失败则调用的视频端口驱动程序会将请求传递给父级的微型端口驱动程序的设备。 如果子驱动程序发送 IRP\_MN\_查询\_到另一个接口未实现的微型端口驱动程序和其他子驱动程序的子*HwVidQueryInterface*或失败的调用中，视频端口驱动程序将返回错误。

因为子驱动程序可以调用的微型端口驱动程序的视频端口驱动程序的不知情的情况下，微型端口驱动程序必须同步到其自身中的所有公开的函数的访问[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface). 这是通过调用[ **VideoPortAcquireDeviceLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportacquiredevicelock)并[ **VideoPortReleaseDeviceLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportreleasedevicelock)获取并释放的视频端口驱动程序维护设备锁定，请分别。

通过枚举子设备[ *HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)。

 

 





