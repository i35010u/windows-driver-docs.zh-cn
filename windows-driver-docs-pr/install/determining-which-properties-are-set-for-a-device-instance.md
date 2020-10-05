---
title: 确定为设备实例设置哪些属性
description: 确定为设备实例设置哪些属性
ms.assetid: aeca4da5-9632-4523-aa2d-8d1c64b1eccc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77b958ad5077594d7803533446ac599aa746f570
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733175"
---
# <a name="determining-which-properties-are-set-for-a-device-instance"></a>确定为设备实例设置哪些属性


若要确定为 Windows Vista 和更高版本的 Windows 上的设备实例设置了哪些属性，请执行以下步骤：

1.  调用 [**SetupDiGetDevicePropertyKeys**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys) ，以确定为设备实例设置了多少个属性。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索属性键列表的设备实例。
    -   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其检索属性键列表的设备实例。
    -   将 *PropertyKeyArray* 设置为 **NULL**。
    -   将 *PropertyKeyCount* 设置为零。
    -   将 *RequiredPropertyKeyCount* 设置为指向 DWORD 类型化变量的指针。
    -   将 *标志* 设置为零。

    在对[**SetupDiGetDevicePropertyKeys**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)的调用做出响应时， **SetupDiGetDevicePropertyKeys**将 \* *RequiredPropertyKeyCount*设置为设备实例设置的属性数，将错误代码记录 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 对 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDevicePropertyKeys** ，并提供在第一次调用中提供的相同参数值，但以下更改除外：

    -   将 *PropertyKeyArray* 设置为 [**DEVPROPKEY**](./devpropkey.md)类型的指针，该指针指向接收请求的属性键数组的缓冲区。
    -   将 *PropertyKeyCount* 设置为 *PropertyKeyArray* 缓冲区的大小，采用 DEVPROPKEY 类型的值。 第一次调用**SetupDiGetDevicePropertyKeys**时，检索到 RequiredPropertyKeyCount 中的*PropertyKeyArray*缓冲区的所需大小 \* *RequiredPropertyKeyCount*。

如果对**SetupDiGetDevicePropertyKeys**的第二次调用成功，则**SetupDiGetDevicePropertyKeys**将返回*PropertyKeyArray*缓冲区中请求的属性键数组，将 \* *RequiredPropertyKeyCount*设置为缓冲区中的属性键的数目，并返回**TRUE**。 如果函数调用失败， **SetupDiGetDevicePropertyKeys** 将返回 **FALSE** ，并且调用 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 将返回记录的错误代码。

