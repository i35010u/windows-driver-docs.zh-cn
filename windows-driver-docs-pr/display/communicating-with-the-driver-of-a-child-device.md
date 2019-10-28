---
title: 与子设备的驱动程序通信
description: 与子设备的驱动程序通信
ms.assetid: f1311941-bfba-44a4-867c-95fcbef19510
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，子设备
- 子设备 WDK 视频微型端口，与驱动程序通信
- HwVidQueryInterface
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54e988f64a4f6f23eecbef1a67c4420c5a3968c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839049"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>与子设备的驱动程序通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


视频微型端口驱动程序和子设备的驱动程序可以相互定义一个接口，该接口允许子驱动程序通过父微型端口驱动程序与其硬件通信。 子驱动程序通过向父微型端口驱动程序的视频端口驱动程序发送[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)请求来获取此接口。 收到此类请求后，视频端口驱动程序将调用微型端口驱动程序的[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)函数（如果已定义），并且微型端口驱动程序将返回指向接口的指针。 然后，子设备的驱动程序可以通过由*HwVidQueryInterface*公开的函数随时调入微型端口驱动程序。

如果微型端口驱动程序未实现[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)或调用失败，则视频端口驱动程序会将请求传递给微型端口驱动程序的设备的父级。 如果子驱动程序将 IRP\_MN\_QUERY\_接口发送到微型端口驱动程序的另一子，而另一个子驱动程序未实现*HwVidQueryInterface*或调用失败，则视频端口驱动程序将返回错误。

由于子驱动程序可以调入微型端口驱动程序，而无需视频端口驱动程序的知识，因此，微型端口驱动程序必须在[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)公开的所有函数中同步对其自身的访问。 为此，可以调用[**VideoPortAcquireDeviceLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportacquiredevicelock)和[**VideoPortReleaseDeviceLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreleasedevicelock) ，分别获取并释放视频端口驱动程序维护的设备锁。

子设备由[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)枚举。

 

 





