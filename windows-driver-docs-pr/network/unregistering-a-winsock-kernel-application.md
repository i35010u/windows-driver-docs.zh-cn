---
title: 取消注册 Winsock 内核应用程序
description: 取消注册 Winsock 内核应用程序
ms.assetid: f5d99c10-eeac-499e-8630-6aa188d38d75
keywords:
- Winsock 内核 WDK 网络，注册
- 注销 Winsock 内核应用程序
- WSK WDK 网络，注册
- WskDeregister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4be9ef5ea2703b3afea0479169ad3e517b80e482
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213161"
---
# <a name="unregistering-a-winsock-kernel-application"></a>取消注册 Winsock 内核应用程序


已成功使用 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 函数注册为 WSK 客户端的 Winsock 内核 (WSK) 应用程序必须确保已调用 [**WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister) ，并在驱动程序的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数返回之前返回了调用。 已成功调用 **WskRegister** 的 WSK 应用程序应在不调用 **WskDeregister**的情况下将其卸载，这将等待取消注册 WSK 客户端对象，直到 WSK 提供程序 NPI 的所有捕获实例都已与 [**WskReleaseProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi) 一起关闭并关闭所有套接字。 如果有等待的 Irp 传递到 [**WSK \_ 提供程序 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)中的函数，则 **WskDeregister** 还会等待这些挂起的 irp 完成。 调用 WskReleaseProviderNPI 后，WSK 应用程序不应调用 WSK \_ 提供程序调度中的函数 \_ 。 **WskReleaseProviderNPI**

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

WSK 应用程序不一定需要始终从其*Unload*函数中调用**WskDeregister** 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则当停用 WSK 应用程序子组件时，可能会出现 WSK 应用程序对 **WskDeregister** 的调用。 在这种情况下，驱动程序从其 *Unload* 函数返回之前，必须确保已使用对 **WskDeregister**的调用成功注销 WSK 应用程序。

 

