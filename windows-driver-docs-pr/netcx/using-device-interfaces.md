---
title: 使用设备接口
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8fbe1ef5d1051c3e59f9fbafe7ab117864cb08a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838268"
---
# <a name="using-device-interfaces"></a>使用设备接口

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

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
