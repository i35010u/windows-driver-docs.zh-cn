---
title: 卸载提供程序模块
description: 卸载提供程序模块
keywords:
- 提供程序模块 WDK 网络模块注册程序，卸载
- 卸载网络模块
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c16fa13f227e5ede2f18cb6c9c98d77924b420f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822770"
---
# <a name="unloading-a-provider-module"></a>卸载提供程序模块


若要卸载提供程序模块，操作系统将调用提供程序模块的 [**unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数。 有关如何在初始化期间指定提供程序模块的 **Unload** 函数的详细信息，请参阅 [初始化和注册提供程序模块](initializing-and-registering-a-provider-module.md)。

提供程序模块的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数确保在从系统内存中卸载提供程序模块之前，从网络模块注册器 (NMR) 中取消注册提供程序模块。 提供程序模块通过调用 [**NmrDeregisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider) 函数开始从 NMR 注销，该函数通常从其 **Unload** 函数调用它。 在从 NMR 中完全取消注册某个提供程序模块之前，该模块不能从其 **Unload** 函数返回。 如果对 **NmrDeregisterProvider** 的调用返回状态 " \_ 挂起"，则提供程序模块必须调用 [**NmrWaitForProviderDeregisterComplete**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforproviderderegistercomplete) 函数以等待注销完成，然后从其 **Unload** 函数返回。

例如：

```C++
// Variable containing the handle for the registration
HANDLE ProviderHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Deregister the provider module from the NMR
  Status =
    NmrDeregisterProvider(
      ProviderHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the deregistration to be completed
    NmrWaitForProviderDeregisterComplete(
      ProviderHandle
      );
  }

  // An error occurred
  else
  {
    // Handle error
    ...
  }
}
```

如果提供程序模块注册为多个 [网络编程接口的提供程序 (NPIs)](network-programming-interface.md)，则它必须为其支持的每个 NPI 调用 [**NmrDeregisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider) 。 如果将网络模块注册为提供程序模块和客户端模块 (也就是说，它是一个 NPI 的提供程序，另一个 NPI) 的客户端，则必须调用 **NmrDeregisterProvider** 和 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)。

在从其 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数返回之前，网络模块必须一直等待，直到所有注销都完成。

提供程序模块不需要从它的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数中调用 [**NmrDeregisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider) 。 例如，如果提供程序模块是复杂驱动程序的子组件，则当激活提供程序模块子组件时，可能会出现提供程序模块的取消注册。 但是，在这种情况下，驱动程序必须确保从 NMR 中完全取消对提供程序模块的注册，然后再从其 **Unload** 函数返回。

 

