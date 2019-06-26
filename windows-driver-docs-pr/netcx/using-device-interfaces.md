---
title: 使用设备接口
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1055fb2e72c8b008569f07d2aff7a193f8f62e5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382808"
---
# <a name="using-device-interfaces"></a>使用设备接口

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

若要从用户模式下接收 Ioctl，客户端驱动程序调用[ **WdfDeviceCreateDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)引用字符串，如下所示：

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
