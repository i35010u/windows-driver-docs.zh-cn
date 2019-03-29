---
title: 检索设备实例标识符
description: 检索设备实例标识符
ms.assetid: 6382fdf6-109a-430a-b6b5-322d3eebc4a1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b52a61d4c7eb3065d71edd94b347fdb219b3be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564781"
---
# <a name="retrieving-a-device-instance-identifier"></a>检索设备实例标识符


在 Windows Vista 和更高版本的 Windows，[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)支持表示设备实例标识符的设备属性。 统一的设备属性模型使用[ **DEVPKEY_Device_InstanceId**](https://msdn.microsoft.com/library/windows/hardware/ff542532) [属性键](property-keys.md)来表示此属性。

Windows Server 2003、 Windows XP 和 Windows 2000 也支持此属性。 但是，这些早期的 Windows 版本不支持统一的设备属性模型的项的属性。 相反，可以通过调用检索这些早期版本的 Windows 上的设备实例标识符[ **SetupDiGetDeviceInstanceId**](https://msdn.microsoft.com/library/windows/hardware/ff551106)。 若要保持与这些早期版本的 Windows 兼容性，Windows Vista 和更高版本还支持**SetupDiGetDeviceInstanceId**。 但是，应使用密钥来访问此属性在 Windows Vista 及更高版本的相应属性。

有关如何使用属性键来访问在 Windows Vista 和更高版本上的设备驱动程序属性的信息，请参阅[访问设备实例属性 （Windows Vista 和更高版本）](accessing-device-instance-properties--windows-vista-and-later-.md)。

若要检索的设备实例标识符在 Windows Server 2003、 Windows XP 和 Windows 2000 上，执行以下步骤：

1.  调用**SetupDiGetDeviceInstanceId**检索大小 （字节） 的设备实例标识符。 提供以下参数值：

    -   设置*DeviceInfoSet*到包含要为其检索请求的设备实例标识符的设备信息元素的设备信息集的句柄。
    -   设置*DeviceInfoData*指向的[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要为其检索设备实例的设备信息元素标识符。
    -   设置*DeviceInstanceId*到**NULL**。
    -   设置*DeviceInstanceIdSize*为零。
    -   设置*RequiredSize*为指向一个 DWORD 类型的变量来接收的以 NULL 结尾的设备实例标识符存储所需的字符数。

    在首次调用的响应[ **SetupDiGetDeviceInstanceId**](https://msdn.microsoft.com/library/windows/hardware/ff551106)， **SetupDiGetDeviceInstanceId**设置\* *RequiredSize*大小，以字节为单位，检索属性值，所需的缓冲区的记录的错误代码 ERROR_INSUFFICIENT_BUFFER，并返回**FALSE**。 随后调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)返回最近记录的错误代码。

2.  调用**SetupDiGetDeviceInstanceId**试并提供在第一个调用中，除以下更改外提供了相同的参数值：
    -   设置*DeviceInstanceId*到指向接收的设备信息元素与关联的以 NULL 结尾的设备实例标识符的字符串缓冲区的指针。
    -   设置*DeviceInstanceIdSize*大小，以字符为单位的*DeviceInstanceId*缓冲区。 首次调用**SetupDiGetDeviceInstanceId**检索所需的大小*DeviceInstanceId*中的缓冲区\* *RequiredSize*。

如果第二个调用**SetupDiGetDeviceInstanceId**成功， **SetupDiGetDeviceInstanceId**设置*DeviceInstanceId*设备实例标识符，缓冲区设置\* *RequiredSize*大小，以字符为单位的设备实例标识符用于已检索，并返回**TRUE**。 如果函数调用失败， **SetupDiGetDeviceInstanceId**返回**FALSE**并调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)返回的记录的错误代码。

 

 





