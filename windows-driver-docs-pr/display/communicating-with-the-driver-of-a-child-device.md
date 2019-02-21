---
title: 使用子设备驱动程序进行通信
description: 使用子设备驱动程序进行通信
ms.assetid: f1311941-bfba-44a4-867c-95fcbef19510
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，子设备
- 子设备 WDK 微型端口，与该驱动程序进行通信
- HwVidQueryInterface
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef481f7de15346760223c990d91c597d0487f55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521449"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>使用子设备驱动程序进行通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


微型端口驱动程序和子设备的驱动程序可以相互定义使子驱动程序与父微型端口驱动程序通过其硬件进行通信的接口。 子驱动程序将获取此接口通过发送[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687)父微型端口驱动程序的视频端口驱动程序的请求。 视频端口驱动程序收到此类请求后，调用微型端口驱动程序[ *HwVidQueryInterface* ](https://msdn.microsoft.com/library/windows/hardware/ff567358)函数，如果定义，并微型端口驱动程序返回对接口的指针。 然后，子设备的驱动程序可以调用到通过公开的函数的微型端口驱动程序*HwVidQueryInterface*在任何时间。

如果微型端口驱动程序不实现[ *HwVidQueryInterface* ](https://msdn.microsoft.com/library/windows/hardware/ff567358)或失败则调用的视频端口驱动程序会将请求传递给父级的微型端口驱动程序的设备。 如果子驱动程序发送 IRP\_MN\_查询\_到另一个接口未实现的微型端口驱动程序和其他子驱动程序的子*HwVidQueryInterface*或失败的调用中，视频端口驱动程序将返回错误。

因为子驱动程序可以调用的微型端口驱动程序的视频端口驱动程序的不知情的情况下，微型端口驱动程序必须同步到其自身中的所有公开的函数的访问[ *HwVidQueryInterface* ](https://msdn.microsoft.com/library/windows/hardware/ff567358). 这是通过调用[ **VideoPortAcquireDeviceLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570174)并[ **VideoPortReleaseDeviceLock** ](https://msdn.microsoft.com/library/windows/hardware/ff570356)获取并释放的视频端口驱动程序维护设备锁定，请分别。

通过枚举子设备[ *HwVidGetVideoChildDescriptor*](https://msdn.microsoft.com/library/windows/hardware/ff567341)。

 

 





