---
title: 创建 KMDF 微型端口驱动程序
description: 创建 KMDF 微型端口驱动程序
ms.assetid: 3e01827b-fe1e-49ce-8072-9fc6c751fc01
keywords:
- 微型端口驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ddf5199e0c440941243fcbfe9ba9f4c827998e9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184045"
---
# <a name="creating-kmdf-miniport-drivers"></a>创建 KMDF 微型端口驱动程序





某些微型端口驱动程序可以使用内核模式驱动程序框架（如果端口/微型端口体系结构允许微型端口驱动程序使用 WDM 或框架接口与其他驱动程序通信）。 例如， [具有 WDM 下边缘的 NDIS 微型端口驱动程序](../network/ndis-miniport-drivers-with-a-wdm-lower-edge.md) 可以使用该框架来实现下边缘。

如果希望微型端口驱动程序使用该框架，驱动程序必须：

-   在调用[**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)之前，请在驱动程序的[**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构的**DriverInitFlags**成员中设置[**WdfDriverInitNoDispatchOverride**](/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags)标志。 设置此标志会使端口驱动程序（而不是框架）拦截 i/o 请求数据包 (Irp) i/o 管理器已定向到该驱动程序。

-   调用 [**WdfDeviceMiniportCreate**](/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate) 而不是 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) ，为微型端口驱动程序的设备创建框架设备对象。 当微型端口驱动程序的端口驱动程序通知其设备可用时，它应调用 **WdfDeviceMiniportCreate** 。

-   当驱动程序确定设备已被删除后，调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 来删除 [**WdfDeviceMiniportCreate**](/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate) 创建的设备对象。  (因为驱动程序已设置 [**WdfDriverInitNoDispatchOverride**](/windows-hardware/drivers/ddi/wdfdriver/ne-wdfdriver-_wdf_driver_init_flags) 标志，所以框架无法确定何时删除设备，也无法删除设备对象。 ) 

-   当端口驱动程序通知微型端口驱动程序即将卸载时，请调用 [**WdfDriverMiniportUnload**](/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdriverminiportunload) 。

只有基础设备支持即插即用 (PnP) 时，微型端口驱动程序才能使用框架。 微型端口驱动程序无法使用框架的控制设备对象。

限制适用于 [**WdfDeviceMiniportCreate**](/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate) 方法创建的设备对象。 有关这些限制的列表，请参阅 [**WdfDeviceMiniportCreate**](/windows-hardware/drivers/ddi/wdfminiport/nf-wdfminiport-wdfdeviceminiportcreate)。

 

