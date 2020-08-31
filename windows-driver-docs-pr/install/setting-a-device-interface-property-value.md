---
title: 设置设备接口属性值
description: 设置设备接口属性值
ms.assetid: 44cef4e1-9fda-44fb-b37f-342099b5f7a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d6b68525266b8c2d0c8930d04d002a03fe8858
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096633"
---
# <a name="setting-a-device-interface-property-value"></a>设置设备接口属性值


若要在 Windows Vista 和更高版本的 Windows 中设置 [设备接口属性](/previous-versions/ff541409(v=vs.85)) 的值，请调用 [**SetupDiSetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw) 并提供以下参数值：

-   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其设置设备接口属性的设备接口。

-   将 *DeviceInterfaceData* 设置为指向 [**SP_DEVICE_INTERFACE_DATA**](/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data) 结构的指针，该结构表示要为其设置设备接口属性的设备接口。

-   将 *PropertyKey* 设置为指向 [**DEVPROPKEY**](./devpropkey.md) 结构的指针，该结构表示要设置的属性。

-   将 *PropertyType* 设置为指向 [**DEVPROPKEY**](./devpropkey.md)类型的变量的指针，该变量提供要设置的属性的属性数据类型标识符。

-   将 *PropertyBuffer* 设置为指向包含属性值的缓冲区的指针。

-   将 *PropertyBufferSize* 设置为属性值的大小（以字节为单位）。

-   将 *RequiredSize* 设置为 DWORD 类型化变量。

-   将 *标志* 设置为零。

如果对 [**SetupDiSetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw) 的调用成功，则 **SetupDiSetDeviceInterfaceProperty** 将设置设备类属性并返回 **TRUE**。 如果函数调用失败， **SetupDiSetDeviceInterfaceProperty** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

 

