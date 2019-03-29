---
title: 设置设备接口属性值
description: 设置设备接口属性值
ms.assetid: 44cef4e1-9fda-44fb-b37f-342099b5f7a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 161d04af5bfe72d8129bdc4b97467570d878fe91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577059"
---
# <a name="setting-a-device-interface-property-value"></a>设置设备接口属性值


若要设置的值[设备接口属性](https://msdn.microsoft.com/library/windows/hardware/ff541409)在 Windows Vista 和更高版本的 Windows 中，调用[ **SetupDiSetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552158)并提供以下参数的值：

-   设置*DeviceInfoSet*到设备的信息集，其中包含要为其设置的设备接口属性的设备接口的句柄。

-   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)结构，它表示要为其设置的设备接口属性的设备接口.

-   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)结构，它表示要设置的属性。

-   设置*PropertyType*指向的[ **DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)-提供要设置的属性的属性数据类型标识符的类型化的变量。

-   设置*PropertyBuffer*到指向包含的属性值的缓冲区的指针。

-   设置*PropertyBufferSize*到大小 （字节） 的属性值。

-   设置*RequiredSize*到 DWORD 类型的变量。

-   设置*标志*为零。

如果在调用[ **SetupDiSetDeviceInterfaceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552158)成功， **SetupDiSetDeviceInterfaceProperty**设置的设备类属性，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiSetDeviceInterfaceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





