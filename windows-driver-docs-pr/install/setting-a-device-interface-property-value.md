---
title: 设置设备接口属性值
description: 设置设备接口属性值
ms.assetid: 44cef4e1-9fda-44fb-b37f-342099b5f7a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0db234ec630d093e175df8f0697ac3b59d91ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378837"
---
# <a name="setting-a-device-interface-property-value"></a>设置设备接口属性值


若要设置的值[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85))在 Windows Vista 和更高版本的 Windows 中，调用[ **SetupDiSetDeviceInterfaceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)并提供以下参数的值：

-   设置*DeviceInfoSet*到设备的信息集，其中包含要为其设置的设备接口属性的设备接口的句柄。

-   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)结构，它表示要为其设置的设备接口属性的设备接口.

-   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)结构，它表示要设置的属性。

-   设置*PropertyType*指向的[ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-提供要设置的属性的属性数据类型标识符的类型化的变量。

-   设置*PropertyBuffer*到指向包含的属性值的缓冲区的指针。

-   设置*PropertyBufferSize*到大小 （字节） 的属性值。

-   设置*RequiredSize*到 DWORD 类型的变量。

-   设置*标志*为零。

如果在调用[ **SetupDiSetDeviceInterfaceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)成功， **SetupDiSetDeviceInterfaceProperty**设置的设备类属性，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiSetDeviceInterfaceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





