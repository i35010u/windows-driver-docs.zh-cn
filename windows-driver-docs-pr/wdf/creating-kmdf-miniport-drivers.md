---
title: 创建 KMDF 微型端口驱动程序
description: 创建 KMDF 微型端口驱动程序
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- 微型端口驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f3f9f6df417eec2488976f1f299e43f7f50ffa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377495"
---
# <a name="creating-kmdf-miniport-drivers"></a>创建 KMDF 微型端口驱动程序





如果端口/微型端口体系结构允许微型端口驱动程序，以使用 WDM 或框架接口与其他驱动程序进行通信，某些微型端口驱动程序可以使用内核模式驱动程序框架。 例如， [WDM 与的 NDIS 微型端口驱动程序降低边缘](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-miniport-drivers-with-a-wdm-lower-edge)可以使用该框架来实现的下边缘。

如果您希望您的微型端口驱动程序以使用该框架，该驱动程序必须：

-   设置[ **WdfDriverInitNoDispatchOverride** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标记中**DriverInitFlags**的驱动程序的成员[ **WDF\_驱动程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)之前，调用结构[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)。 设置此标志后，端口驱动程序，改为的框架，为截距 I/O 请求数据包 (Irp) I/O 管理器已定向到该驱动程序。

-   调用[ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)而不是[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)创建设备对象的微型端口驱动程序的框架设备。 微型端口驱动程序应调用**WdfDeviceMiniportCreate**时其端口驱动程序会通知其即用设备。

-   调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)若要删除设备对象的[ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)时驱动程序确定的创建已删除设备。 (因为驱动程序已设置[ **WdfDriverInitNoDispatchOverride** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标志，该框架时删除该设备不能确定，则不能删除设备对象。)

-   调用[ **WdfDriverMiniportUnload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdriverminiportunload)时端口驱动程序通知了微型端口驱动程序，它是即将卸载。

微型端口驱动程序可以使用该框架，仅当基础设备支持插即用 (PnP)。 微型端口驱动程序不能使用框架的控制设备对象。

限制应用于设备的对象的[ **WdfDeviceMiniportCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)方法创建。 有关这些限制的列表，请参阅[ **WdfDeviceMiniportCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)。

 

 





