---
title: 使用设备接口
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da0b80e0575791256169f7c5ddf7e5328dbc2cf3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575653"
---
# <a name="using-device-interfaces"></a>使用设备接口

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

若要从用户模式下接收 Ioctl，客户端驱动程序调用[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)引用字符串，如下所示：

```cpp
DECLARE_CONST_UNICODE_STRING(c_RefString, L"MyRefString");
status = WdfDeviceCreateDeviceInterface(
            device, 
            &GUID_MY_DEVICE_INTERFACE, 
            &c_RefString);
if (!NT_SUCCESS(status)) {
    return status;
}
```

当在用户模式应用程序将请求发送到设备接口的引用字符串上打开的句柄时，客户端驱动程序接收的 I/O 请求。  可以使用[WDF 队列对象](../wdf/framework-queue-objects.md)来处理传入的 I/O 请求。  如果未提供引用字符串，NDIS 截获发送到设备接口的 I/O 请求。

有关详细信息，请参阅[使用 WDF 设备接口](../wdf/using-device-interfaces.md)。
