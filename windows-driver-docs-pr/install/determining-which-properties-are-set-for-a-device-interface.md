---
title: 确定为设备接口设置哪些属性
description: 确定为设备接口设置哪些属性
ms.assetid: ef261c1d-0715-4501-b2db-fab270cee010
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9a1bd88ad8ab61fe2e1e40d1054586a368b4c77
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106592"
---
# <a name="determining-which-properties-are-set-for-a-device-interface"></a>确定为设备接口设置哪些属性


若要确定在 Windows Vista 和更高版本的 Windows 中为设备接口设置了哪些属性，请执行以下步骤：

1.  调用 [**SetupDiGetDeviceInterfacePropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys) ，以确定为设备类设置了多少个属性。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索设备接口属性密钥列表的设备接口实例。
    -   将 *DeviceInterfaceData* 设置为指向 [**SP_DEVICE_INTERFACE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构的指针，该结构表示要为其检索设备属性键列表的设备接口实例。
    -   将 *PropertyKeyArray* 设置为 **NULL**。
    -   将 *PropertyKeyCount* 设置为零。
    -   将 *RequiredPropertyKeyCount* 设置为指向 DWORD 类型化变量的指针。
    -   将标志设置为零。

    为响应对[**SetupDiGetDeviceInterfacePropertyKeys**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)的此调用， **SetupDiGetDeviceInterfacePropertyKeys**将 \* *RequiredPropertyKeyCount*设置为设备接口的属性数，将错误代码记录 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDeviceInterfacePropertyKeys** ，并提供在第一次调用中提供的相同参数值，但以下更改除外：
    -   将 *PropertyKeyArray* 设置为 [**DEVPROPKEY**](./devpropkey.md)类型的指针，该指针指向接收请求的属性键数组的缓冲区。
    -   将 *PropertyKeyCount* 设置为 *PropertyKeyArray* 缓冲区的大小，采用 DEVPROPKEY 类型的值。 第一次调用**SetupDiGetDeviceInterfacePropertyKeys**时，检索到 RequiredPropertyKeyCount 中的*PropertyKeyArray*缓冲区的所需大小 \* *RequiredPropertyKeyCount*。

如果对**SetupDiGetDeviceInterfacePropertyKeys**的第二次调用成功，则**SetupDiGetDeviceInterfacePropertyKeys**将返回*PropertyKeyArray*缓冲区中请求的属性键数组，将 \* *RequiredPropertyKeyCount*设置为缓冲区中的属性键的数目，并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceInterfacePropertyKeys** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

 

