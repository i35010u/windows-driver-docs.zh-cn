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
ms.openlocfilehash: 23906d3ad428fd579df691b9b4736eaea6859e67
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064390"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>与子设备的驱动程序通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


视频微型端口驱动程序和子设备的驱动程序可以相互定义一个接口，该接口允许子驱动程序通过父微型端口驱动程序与其硬件通信。 子驱动程序通过向父微型端口驱动程序的视频端口驱动程序发送 [**IRP \_ MN \_ 查询 \_ 接口**](../kernel/irp-mn-query-interface.md) 请求来获取此接口。 收到此类请求后，视频端口驱动程序将调用微型端口驱动程序的 [*HwVidQueryInterface*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface) 函数（如果已定义），并且微型端口驱动程序将返回指向接口的指针。 然后，子设备的驱动程序可以通过由 *HwVidQueryInterface* 公开的函数随时调入微型端口驱动程序。

如果微型端口驱动程序未实现 [*HwVidQueryInterface*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface) 或调用失败，则视频端口驱动程序会将请求传递给微型端口驱动程序的设备的父级。 如果子驱动程序将 IRP \_ MN \_ 查询接口发送 \_ 到小型端口驱动程序的另一子，而另一个子驱动程序未实现 *HwVidQueryInterface* 或调用失败，则视频端口驱动程序将返回错误。

由于子驱动程序可以调入微型端口驱动程序，而无需视频端口驱动程序的知识，因此，微型端口驱动程序必须在 [*HwVidQueryInterface*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)公开的所有函数中同步对其自身的访问。 为此，可以调用 [**VideoPortAcquireDeviceLock**](/windows-hardware/drivers/ddi/video/nf-video-videoportacquiredevicelock) 和 [**VideoPortReleaseDeviceLock**](/windows-hardware/drivers/ddi/video/nf-video-videoportreleasedevicelock) ，分别获取并释放视频端口驱动程序维护的设备锁。

子设备由 [*HwVidGetVideoChildDescriptor*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)枚举。

 

