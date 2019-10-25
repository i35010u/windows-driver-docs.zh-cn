---
title: 访问统一的设备属性模型
description: 本主题介绍 Windows 驱动程序框架（WDF）驱动程序如何检索或修改通过统一设备属性模型公开的属性。
ms.assetid: C81988F9-E0DA-439F-B770-DAD86E33D5F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 041a1aeb18f417948d6ce3a611802e9217b83aa0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845514"
---
# <a name="accessing-the-unified-device-property-model"></a>访问统一的设备属性模型


本主题介绍 Windows 驱动程序框架（WDF）驱动程序如何检索或修改通过统一设备属性模型公开的属性。 列出的方法可从用户模式驱动程序框架（UMDF）版本2.0 和内核模式驱动程序框架（KMDF）版本1.13 开始使用。

KMDF 和 UMDF 驱动程序都可以调用以下方法：

-   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
-   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
-   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)

KMDF 和 UMDF 驱动程序只能在调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之前调用以下方法。 有关调用**WdfDeviceCreate**的详细信息，请参阅[创建框架设备对象](creating-a-framework-device-object.md)。

调用[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)之后，驱动程序可以通过调用相应的**WdfDevice*Xxx*属性**方法来获取设备属性信息。

-   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
-   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

上面的 *-ex*方法不同于它们的非*Ex*方法，因为它们允许你使用[**WDF\_设备\_属性\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_property_data)结构来指定属性，而不是使用[**可指定的子集设备\_注册表\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ne-wudfwdm-device_registry_property)。

在接收设备属性数据之前，驱动程序通常只调用**Wdf*Xxx*QueryProperty**来获取所需的缓冲区大小。 对于某些属性，数据大小会在返回所需大小和驱动程序再次调用**Wdf*Xxx*QueryProperty**之间发生变化。 因此，驱动程序应在执行的循环中调用**Wdf*Xxx*QueryProperty** ，直到返回状态 **\_缓冲区\_\_太小**。

仅当所需的缓冲区大小已知且不发生变化时，才最好使用**Wdf*xxx*QueryProperty** ，因为在这种情况下，驱动程序必须只调用**Wdf*xxx*QueryProperty**一次。 如果所需的缓冲区大小未知或不同，则驱动程序应调用**Wdf*Xxx*AllocAndQueryProperty**。

## <a name="accessing-device-interface-properties"></a>访问设备接口属性


UMDF 驱动程序可以使用以下方法检索或修改通过统一属性模型公开的[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))：

-   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
-   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
-   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)

若要检索或修改设备接口属性，KMDF 驱动程序必须直接调用[**IoGetDeviceInterfacePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacepropertydata)或[**IoSetDeviceInterfacePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacepropertydata) 。

 

 





