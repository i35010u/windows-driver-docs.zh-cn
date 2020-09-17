---
title: 检索设备接口属性值
description: 检索设备接口属性值
ms.assetid: 2a845adc-6965-420d-9e0a-20935d20577a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c827e3f6b85a07ee1f0680c574c13563a02e7a9a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715430"
---
# <a name="retrieving-a-device-interface-property-value"></a>检索设备接口属性值


从 Windows Vista 开始，按照以下步骤检索 [设备接口属性](/previous-versions/ff541409(v=vs.85))的值：

1.  调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 以确定属性值的数据类型和大小（以字节为单位）。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索设备接口属性密钥列表的设备接口。
    -   将 *DeviceInterfaceData* 设置为指向 [**SP_DEVICE_INTERFACE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构的指针，该结构表示要为其检索设备属性键列表的设备接口。
    -   将 *PropertyKey* 设置为指向表示属性的 [**DEVPROPKEY**](./devpropkey.md) 结构的指针。
    -   将 *PropertyType* 设置为指向 [**DEVPROPKEY**](./devpropkey.md)类型的变量的指针。
    -   将 *PropertyBuffer* 设置为 **NULL**。
    -   将 *PropertyBufferSize* 设置为零。
    -   将 *RequiredSize* 设置为 DWORD 类型化变量。
    -   将标志设置为零。

    在对[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)的第一次调用时， **SetupDiGetDeviceInterfaceProperty**将 \* *RequiredSize*设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回**FALSE**。 对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDeviceInterfaceProperty** ，并提供与第一次调用提供的参数值相同的参数值，如下所示：
    -   将 *PropertyBuffer* 设置为指向接收属性值的缓冲区的指针。
    -   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区的所需大小（以字节为单位）。 第一次调用**SetupDiGetDeviceInterfaceProperty**时，检索到 RequiredSize 中的*PropertyBuffer*缓冲区的所需大小 \* *RequiredSize*。

如果对**SetupDiGetDeviceInterfaceProperty**的第二次调用成功，则**SetupDiGetDeviceInterfaceProperty**将 \* *PropertyType*设置为属性的属性数据类型标识符，将*PropertyBuffer*缓冲区设置为属性值，将 \* *RequiredSize*设置为检索到的属性值的大小（以字节为单位），并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceInterfaceProperty** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

 

