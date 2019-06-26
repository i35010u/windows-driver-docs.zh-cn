---
title: 取消注册 Winsock 内核应用程序
description: 取消注册 Winsock 内核应用程序
ms.assetid: f5d99c10-eeac-499e-8630-6aa188d38d75
keywords:
- Winsock 内核 WDK 连接网络、 注册
- 正在注销 Winsock 内核应用程序
- WSK WDK 连接网络、 注册
- WskDeregister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebe949c8459828704bdeb9eb6f65b7700870d9b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386828"
---
# <a name="unregistering-a-winsock-kernel-application"></a>取消注册 Winsock 内核应用程序


已成功注册为 WSK 客户端使用的 Winsock Kernel (WSK) 应用程序[ **WskRegister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskregister)函数必须确保[ **WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskderegister)已调用，并调用已返回之前的驱动程序, [**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)函数返回。 已调用的 WSK 应用程序**WskRegister**成功应永远不会卸载而无需调用**WskDeregister**，这将等待直到所有捕获实例的注销 WSK 客户端对象在发布时提供程序 WSK NPI [ **WskReleaseProviderNPI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/nf-wsk-wskreleaseprovidernpi)和所有套接字关闭 WSK 应用程序。 如果有挂起的已传递到函数中的 Irp [ **WSK\_提供程序\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wsk/ns-wsk-_wsk_provider_dispatch)， **WskDeregister**还将等待，直到这些挂起的 Irp 完成。 WSK 应用程序应永远不会在 WSK 中调用函数\_提供程序\_调度后**WskReleaseProviderNPI**调用。

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

WSK 应用程序不一定需要始终调用**WskDeregister**从其*卸载*函数。 例如，如果 WSK 应用程序是一个复杂的驱动程序，WSK 应用程序的调用的子组件**WskDeregister** WSK 应用程序子组件将停用时可能发生。 在此类方案中之前从驱动程序将返回, 其*Unload*函数，它仍须确保 WSK 应用程序已通过调用已成功注销**WskDeregister**。

 

 





