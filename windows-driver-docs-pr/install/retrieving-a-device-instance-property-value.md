---
title: 检索设备实例属性值
description: 检索设备实例属性值
ms.assetid: 4cec9132-5a28-492d-bbb1-39e388413ad0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d14fe31c3d4d79cd6b8b8f4fab68df2e7a44b7e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555276"
---
# <a name="retrieving-a-device-instance-property-value"></a>检索设备实例属性值


若要检索的 Windows Vista 上的设备实例属性值和更高版本的 Windows，请执行以下步骤：

1.  调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)来确定数据类型和大小 （字节） 的属性值。 提供以下参数值：

    -   设置*DeviceInfoSet*到设备的信息集，其中包含要为其检索属性的设备实例的句柄。
    -   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其检索属性的设备实例。
    -   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)结构，它表示该属性。
    -   设置*PropertyType*指向的[ **DEVPROPTYPE**](https://msdn.microsoft.com/library/windows/hardware/ff543546)-类型化的变量中。
    -   设置*PropertyBuffer*到**NULL**。
    -   设置*PropertyBufferSize*为零。
    -   设置*RequiredSize*到指向 DWORD 类型的变量的指针。
    -   设置*标志*为零。

    在首次调用的响应[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)， **SetupDiGetDeviceProperty**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDeviceProperty**试并提供在第一个调用中，除以下更改外提供了相同的参数值：
    -   设置*PropertyBuffer*到指向该缓冲区用于接收的属性值的指针。
    -   设置*PropertyBufferSize*到所需的大小，以字节为单位的*PropertyBuffer*缓冲区。 首次调用**SetupDiGetDeviceProperty**检索所需的大小*PropertyBuffer*中的缓冲区\* *RequiredSize*。

如果第二个调用**SetupDiGetDeviceProperty**成功， **SetupDiGetDeviceProperty**设置\* *PropertyType*为属性数据类型属性标识符中的属性值返回*PropertyBuffer*缓冲集\* *RequiredSize*的大小，以字节为单位，属性值的表格是检索，并返回 **，则返回 TRUE**。 如果函数调用失败， **SetupDiGetDeviceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





