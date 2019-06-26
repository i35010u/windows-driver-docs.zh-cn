---
title: 访问统一的设备属性模型
description: 本主题介绍如何将 Windows 驱动程序框架 (WDF) 驱动程序中检索或修改通过统一的设备属性模型公开的属性。
ms.assetid: C81988F9-E0DA-439F-B770-DAD86E33D5F3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ae5f6d8211f5dc16867b75e9b29fe45043b3a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379052"
---
# <a name="accessing-the-unified-device-property-model"></a>访问统一的设备属性模型


本主题介绍如何将 Windows 驱动程序框架 (WDF) 驱动程序中检索或修改通过统一的设备属性模型公开的属性。 列出的方法是在用户模式驱动程序框架 (UMDF) 2.0 版和内核模式驱动程序框架 (KMDF) 版本 1.13 中推出。

KMDF 和 UMDF 驱动程序可以调用以下方法：

-   [**WdfDeviceAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandquerypropertyex)
-   [**WdfDeviceAssignProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassignproperty)
-   [**WdfDeviceQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequerypropertyex)

KMDF 和 UMDF 驱动程序可以调用以下方法之前调用仅[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)。 有关调用详细信息**WdfDeviceCreate**，请参阅[创建 Framework 设备对象](creating-a-framework-device-object.md)。

在调用[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)，驱动程序可以获取通过调用相应的设备属性信息**WdfDevice*Xxx*属性**方法。

-   [**WdfFdoInitAllocAndQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitallocandquerypropertyex)
-   [**WdfFdoInitQueryPropertyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitquerypropertyex)

*-Ex*上述方法不同于其非 *-Ex*对应的中，它们允许您使用指定属性[ **WDF\_设备\_属性\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_property_data)结构，而不是使用指定的子集[**设备\_注册表\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ne-wudfwdm-device_registry_property).

接收设备属性数据之前, 的驱动程序通常情况下调用**Wdf*Xxx*QueryProperty**只是为了获取所需的缓冲区大小。 对于某些属性，数据大小可以当返回所需的大小和当驱动程序调用之间切换**Wdf*Xxx*QueryProperty**试。 因此，驱动程序应调用**Wdf*Xxx*QueryProperty**在执行，直到返回的状态不是一个循环内**状态\_缓冲区\_过\_小型**。

最好是使用**Wdf*Xxx*QueryProperty**仅当所需的缓冲区大小是已知的和不变，因为在这种情况下，驱动程序必须调用**Wdf*Xxx*QueryProperty**仅一次。 如果所需的缓冲区大小是未知的或各不相同，则驱动程序应调用**Wdf*Xxx*AllocAndQueryProperty**。

## <a name="accessing-device-interface-properties"></a>访问设备接口属性


UMDF 驱动程序可以使用以下方法来检索或修改[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))通过统一的属性模型公开：

-   [**WdfDeviceAllocAndQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceallocandqueryinterfaceproperty)
-   [**WdfDeviceAssignInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigninterfaceproperty)
-   [**WdfDeviceQueryInterfaceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicequeryinterfaceproperty)

若要检索或修改设备接口属性，KMDF 驱动程序必须调用[ **IoGetDeviceInterfacePropertyData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfacepropertydata)或[ **IoSetDeviceInterfacePropertyData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacepropertydata)直接。

 

 





