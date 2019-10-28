---
title: 注销 Winsock 内核应用程序
description: 注销 Winsock 内核应用程序
ms.assetid: f5d99c10-eeac-499e-8630-6aa188d38d75
keywords:
- Winsock 内核 WDK 网络，注册
- 注销 Winsock 内核应用程序
- WSK WDK 网络，注册
- WskDeregister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 712c802c6c91451981855328010f0d9785a0b3c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843004"
---
# <a name="unregistering-a-winsock-kernel-application"></a>注销 Winsock 内核应用程序


已成功注册为具有[**WskRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)函数的 WSK 客户端的 Winsock 内核（WSK）应用程序必须确保已调用[**WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister) ，并在驱动程序的[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数返回之前返回调用. 已成功调用**WskRegister**的 WSK 应用程序永远不应在不调用**WskDeregister**的情况下卸载，这将等待取消注册 WSK 客户端对象，直到 WSK 提供程序 NPI 的所有捕获实例都已释放[ **。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)WSK 应用程序关闭了 WskReleaseProviderNPI 和所有套接字。 如果有一些挂起的 Irp 已传递到 WSK 中的函数[ **\_提供程序\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)，则**WskDeregister**还会等待这些挂起的 irp 完成。 调用**WskReleaseProviderNPI**后，WSK 应用程序不应\_调度\_调用程序中的函数。

例如：

```C++
// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  // Unregister the WSK application
  WskDeregister(
    &WskRegistration
    );

}
```

WSK 应用程序不一定需要始终从其*Unload*函数中调用**WskDeregister** 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则当停用 WSK 应用程序子组件时，可能会出现 WSK 应用程序对**WskDeregister**的调用。 在这种情况下，驱动程序从其*Unload*函数返回之前，必须确保已使用对**WskDeregister**的调用成功注销 WSK 应用程序。

 

 





