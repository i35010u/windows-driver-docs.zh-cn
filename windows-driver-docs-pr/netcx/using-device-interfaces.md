---
title: 使用设备接口
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6cd0f66e44cbb7eb33c067d3d0a7128147e4a744
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208935"
---
# <a name="using-device-interfaces"></a>使用设备接口

若要从用户模式接收 IOCTLs，客户端驱动程序将使用引用字符串调用[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) ，如下所示：

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

当用户模式应用程序将请求发送到使用引用字符串在设备接口上打开的句柄时，客户端驱动程序将接收 i/o 请求。  可以使用[WDF 队列对象](../wdf/framework-queue-objects.md)处理传入的 i/o 请求。  如果未提供引用字符串，NDIS 会截获发送到设备接口的 i/o 请求。

有关详细信息，请参阅[使用 WDF 设备接口](../wdf/using-device-interfaces.md)。
