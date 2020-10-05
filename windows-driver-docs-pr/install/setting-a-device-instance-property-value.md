---
title: 设置设备实例属性值
description: 设置设备实例属性值
ms.assetid: 45f63ee3-278e-4b8c-a666-c860074fa172
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b15464b39d0cda7733d8e675b7b28ae04e5dbe0
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733671"
---
# <a name="setting-a-device-instance-property-value"></a>设置设备实例属性值


若要在 Windows Vista 和更高版本的 Windows 上设置设备实例属性的值，请调用 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 并提供以下参数值：

-   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其设置属性的设备实例。

-   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其设置属性的设备实例。

-   将 *PropertyKey* 设置为指向 [**DEVPROPKEY**](./devpropkey.md) 结构的指针，该结构表示要设置的属性。

-   将 *PropertyType* 设置为指向 [**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))类型的变量的指针，该变量提供要设置的属性的属性数据类型标识符。

-   将 *PropertyBuffer* 设置为指向包含属性值的缓冲区的指针。

-   将 *PropertyBufferSize* 设置为属性值的大小（以字节为单位）。

-   将 *RequiredSize* 设置为 DWORD 类型化变量。

-   将 *标志* 设置为零。

如果对 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw) 的此调用成功，则 **SetupDiSetDeviceProperty** 将设置设备实例属性并返回 **TRUE**。 如果函数调用失败， **SetupDiGetDeviceProperty** 将返回 **FALSE** ，并且对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的调用将返回记录的错误代码。

