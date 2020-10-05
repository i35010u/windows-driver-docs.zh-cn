---
title: 检索设备实例属性值
description: 检索设备实例属性值
ms.assetid: 4cec9132-5a28-492d-bbb1-39e388413ad0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8837c741c531475a34e3935c938b4bbc037693af
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732523"
---
# <a name="retrieving-a-device-instance-property-value"></a>检索设备实例属性值


若要在 Windows Vista 和更高版本的 Windows 上检索设备实例属性的值，请执行以下步骤：

1.  调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 以确定属性值的数据类型和大小（以字节为单位）。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索属性的设备实例。
    -   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其检索属性的设备实例。
    -   将 *PropertyKey* 设置为指向表示属性的 [**DEVPROPKEY**](./devpropkey.md) 结构的指针。
    -   将 *PropertyType* 设置为指向 [**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))类型的变量的指针。
    -   将 *PropertyBuffer* 设置为 **NULL**。
    -   将 *PropertyBufferSize* 设置为零。
    -   将 *RequiredSize* 设置为指向 DWORD 类型化变量的指针。
    -   将 *标志* 设置为零。

    在对[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)的第一次调用时， **SetupDiGetDeviceProperty**将 \* *RequiredSize*设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回**FALSE**。 对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDeviceProperty** ，并提供在第一次调用中提供的相同参数值，但以下更改除外：
    -   将 *PropertyBuffer* 设置为指向接收属性值的缓冲区的指针。
    -   将 *PropertyBufferSize* 设置为 *PropertyBuffer* 缓冲区的所需大小（以字节为单位）。 第一次调用**SetupDiGetDeviceProperty**时，检索到 RequiredSize 中的*PropertyBuffer*缓冲区的所需大小 \* *RequiredSize*。

如果对**SetupDiGetDeviceProperty**的第二次调用成功，则**SetupDiGetDeviceProperty**将 \* *PropertyType*设置为属性的属性数据类型标识符，返回*PropertyBuffer*缓冲区中的属性值，将 \* *RequiredSize*设置为检索到的属性值的大小（以字节为单位），并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceProperty** 将返回 **FALSE** ，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

