---
title: 检索设备接口属性值
description: 检索设备接口属性值
ms.assetid: 2a845adc-6965-420d-9e0a-20935d20577a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ca3685b78652bd2e5e4a3bc631343961d95a410
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378037"
---
# <a name="retrieving-a-device-interface-property-value"></a>检索设备接口属性值


从 Windows Vista 开始按照以下步骤检索的值[设备接口属性](https://docs.microsoft.com/previous-versions/ff541409(v=vs.85)):

1.  调用[ **SetupDiGetDeviceInterfaceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)来确定数据类型和大小 （字节） 的属性值。 提供以下参数值：

    -   设置*DeviceInfoSet*到设备的信息集，其中包含要检索的设备接口属性键列表的设备接口的句柄。
    -   设置*DeviceInterfaceData*指向的[ **SP_DEVICE_INTERFACE_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_device_interface_data)结构，它表示要为其检索一组设备的设备接口属性键。
    -   设置*PropertyKey*指向的[ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)结构，它表示该属性。
    -   设置*PropertyType*指向的[ **DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)-类型化的变量中。
    -   设置*PropertyBuffer*到**NULL**。
    -   设置*PropertyBufferSize*为零。
    -   设置*RequiredSize*到 DWORD 类型的变量。
    -   将标志设置为零。

    在首次调用的响应[ **SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)， **SetupDiGetDeviceInterfaceProperty**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回最近记录的错误代码。

2.  调用**SetupDiGetDeviceInterfaceProperty**试并提供相同的参数值提供到第一个调用时，除了以下更改：
    -   设置*PropertyBuffer*到指向该缓冲区用于接收的属性值的指针。
    -   设置*PropertyBufferSize*到所需的大小，以字节为单位的*PropertyBuffer*缓冲区。 首次调用**SetupDiGetDeviceInterfaceProperty**检索所需的大小*PropertyBuffer*中的缓冲区\* *RequiredSize*。

如果第二个调用**SetupDiGetDeviceInterfaceProperty**成功， **SetupDiGetDeviceInterfaceProperty**设置\* *PropertyType*到属性数据类型标识符的属性，设置*PropertyBuffer*属性值设置到缓冲区\* *RequiredSize*到大小 （字节） 属性已检索，并返回值 **，则返回 TRUE**。 如果函数调用失败， **SetupDiGetDeviceInterfaceProperty**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)将返回的记录的错误代码。

 

 





