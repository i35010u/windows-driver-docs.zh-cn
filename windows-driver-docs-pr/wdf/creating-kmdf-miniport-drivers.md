---
title: 创建 KMDF 微型端口驱动程序
description: 创建 KMDF 微型端口驱动程序
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- 微型端口驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2253b9d48be2a68d6d055a0e89b5e0f43385df6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358553"
---
# <a name="creating-kmdf-miniport-drivers"></a>创建 KMDF 微型端口驱动程序





如果端口/微型端口体系结构允许微型端口驱动程序，以使用 WDM 或框架接口与其他驱动程序进行通信，某些微型端口驱动程序可以使用内核模式驱动程序框架。 例如， [WDM 与的 NDIS 微型端口驱动程序降低边缘](https://msdn.microsoft.com/library/windows/hardware/ff565954)可以使用该框架来实现的下边缘。

如果您希望您的微型端口驱动程序以使用该框架，该驱动程序必须：

-   设置[ **WdfDriverInitNoDispatchOverride** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)标记中**DriverInitFlags**的驱动程序的成员[ **WDF\_驱动程序\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)之前，调用结构[ **WdfDriverCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547175)。 设置此标志后，端口驱动程序，改为的框架，为截距 I/O 请求数据包 (Irp) I/O 管理器已定向到该驱动程序。

-   调用[ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)而不是[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)创建设备对象的微型端口驱动程序的框架设备。 微型端口驱动程序应调用**WdfDeviceMiniportCreate**时其端口驱动程序会通知其即用设备。

-   调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)若要删除设备对象的[ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)时驱动程序确定的创建已删除设备。 (因为驱动程序已设置[ **WdfDriverInitNoDispatchOverride** ](https://msdn.microsoft.com/library/windows/hardware/ff551303)标志，该框架时删除该设备不能确定，则不能删除设备对象。)

-   调用[ **WdfDriverMiniportUnload** ](https://msdn.microsoft.com/library/windows/hardware/ff547193)时端口驱动程序通知了微型端口驱动程序，它是即将卸载。

微型端口驱动程序可以使用该框架，仅当基础设备支持插即用 (PnP)。 微型端口驱动程序不能使用框架的控制设备对象。

限制应用于设备的对象的[ **WdfDeviceMiniportCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546802)方法创建。 有关这些限制的列表，请参阅[ **WdfDeviceMiniportCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546802)。

 

 





