---
title: 检索设备实例标识符
description: 检索设备实例标识符
ms.assetid: 6382fdf6-109a-430a-b6b5-322d3eebc4a1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5840a8eaa3efc2a56842dd9b12133856422aa6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106486"
---
# <a name="retrieving-a-device-instance-identifier"></a>检索设备实例标识符


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持表示设备实例标识符的设备属性。 统一设备属性模型使用 [**DEVPKEY_Device_InstanceId**](./devpkey-device-instanceid.md) [属性键](property-keys.md) 来表示此属性。

Windows Server 2003、Windows XP 和 Windows 2000 还支持此属性。 但是，这些早期版本的 Windows 版本不支持统一设备属性模型的属性键。 相反，可以通过调用 [**SetupDiGetDeviceInstanceId**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)在这些早期版本的 Windows 上检索设备实例标识符。 为了保持与这些早期版本的 Windows 的兼容性，Windows Vista 及更高版本也支持 **SetupDiGetDeviceInstanceId**。 但是，在 Windows Vista 和更高版本中，你应使用相应的属性键来访问此属性。

有关如何使用属性键访问 Windows Vista 和更高版本上的设备驱动程序属性的信息，请参阅 [ (Windows vista 和更高版本) 访问设备实例属性 ](accessing-device-instance-properties--windows-vista-and-later-.md)。

若要在 Windows Server 2003、Windows XP 和 Windows 2000 上检索设备实例标识符，请执行以下步骤：

1.  调用 **SetupDiGetDeviceInstanceId** 可检索设备实例标识符的大小（以字节为单位）。 提供以下参数值：

    -   将 *DeviceInfoSet* 设置为设备信息集的句柄，其中包含要为其检索请求的设备实例标识符的设备信息元素。
    -   将 *DeviceInfoData* 设置为指向 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构的指针，该结构表示要为其检索设备实例标识符的设备信息元素。
    -   将 *DeviceInstanceId* 设置为 **NULL**。
    -   将 *DeviceInstanceIdSize* 设置为零。
    -   将 *RequiredSize* 设置为指向 DWORD 类型的变量的指针，该变量接收存储以 NULL 结尾的设备实例标识符所需的字符数。

    在对[**SetupDiGetDeviceInstanceId**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)的第一次调用时， **SetupDiGetDeviceInstanceId**将 \* *RequiredSize*设置为检索属性值所需的缓冲区大小（以字节为单位），记录错误代码 ERROR_INSUFFICIENT_BUFFER 并返回**FALSE**。 对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的后续调用将返回最近记录的错误代码。

2.  再次调用 **SetupDiGetDeviceInstanceId** ，并提供在第一次调用中提供的相同参数值，但以下更改除外：
    -   将 *DeviceInstanceId* 设置为指向字符串缓冲区的指针，该字符串缓冲区接收与设备信息元素关联的以 NULL 结尾的设备实例标识符。
    -   将 *DeviceInstanceIdSize* 设置为 *DeviceInstanceId* 缓冲区的大小（以字符为字符）。 第一次调用**SetupDiGetDeviceInstanceId**时，检索到 RequiredSize 中的*DeviceInstanceId*缓冲区的所需大小 \* *RequiredSize*。

如果对**SetupDiGetDeviceInstanceId**的第二次调用成功，则**SetupDiGetDeviceInstanceId**将*DeviceInstanceId*缓冲区设置为设备实例标识符，将 \* *RequiredSize*设置为检索到的设备实例标识符的大小（以字符为字符），并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceInstanceId** 将返回 **FALSE** ，并且对 [GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416) 的调用将返回记录的错误代码。

 

