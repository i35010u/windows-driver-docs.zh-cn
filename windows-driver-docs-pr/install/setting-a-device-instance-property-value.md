---
title: 设置设备实例属性值
description: 设置设备实例属性值
ms.assetid: 45f63ee3-278e-4b8c-a666-c860074fa172
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eddc4aa09a80623892db2651363fdb8e097dd471
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575449"
---
# <a name="setting-a-device-instance-property-value"></a>设置设备实例属性值


若要在 Windows Vista 和更高版本的 Windows 上设置设备实例属性的值，调用[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163) ，并提供以下参数值：

-   设置*DeviceInfoSet*到设备的信息集，其中包含要为其设置属性的设备实例的句柄。

-   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其设置属性的设备实例。

-   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)结构，它表示要设置的属性。

-   设置*PropertyType*指向的[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-提供要设置的属性的属性数据类型标识符的类型化的变量。

-   设置*PropertyBuffer*到指向包含的属性值的缓冲区的指针。

-   设置*PropertyBufferSize*到大小 （字节） 的属性值。

-   设置*RequiredSize*到 DWORD 类型的变量。

-   设置*标志*为零。

如果此调用[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)成功， **SetupDiSetDeviceProperty**设置的设备实例属性，并返回**TRUE**. 如果函数调用失败， **SetupDiGetDeviceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





