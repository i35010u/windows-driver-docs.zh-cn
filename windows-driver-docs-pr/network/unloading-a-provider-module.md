---
title: 卸载提供程序模块
description: 卸载提供程序模块
ms.assetid: c6dd6552-2923-4091-9bf1-5833c049aa23
keywords:
- 提供程序模块 WDK 网络模块注册机构，卸载
- 正在卸载的网络模块
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38b9a99993b2c8fc20d9c322c319ff487cc6454a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366135"
---
# <a name="unloading-a-provider-module"></a>卸载提供程序模块


若要卸载提供程序模块，操作系统将调用提供程序模块[**卸载**](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 请参阅[初始化和注册提供程序模块](initializing-and-registering-a-provider-module.md)有关如何指定提供程序模块的详细信息**卸载**在初始化过程中的函数。

提供程序模块[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数还可确保从系统内存中卸载提供程序模块之前，以此提供程序模块从网络模块注册机构 (NMR)。 启动从 NMR 注销通过调用提供程序模块[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)函数，它通常会调用从其**卸载**函数。 提供程序模块不能返回从其**Unload**后它具有已完全取消注册从 NMR 直到正常。 如果在调用**NmrDeregisterProvider**将返回状态\_挂起状态，必须调用提供程序模块[ **NmrWaitForProviderDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568787)函数等待注销完成之前它将返回其**Unload**函数。

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

如果为多个提供程序注册提供程序模块[网络编程接口 (NPIs)](network-programming-interface.md)，它必须调用[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)为每个 NPI 它支持。 如果网络模块已注册为提供程序模块和客户端模块 （也就是说，它是一个 NPI 的提供程序和客户端的另一个 NPI），它必须同时调用**NmrDeregisterProvider**并[ **NmrDeregisterClient**](https://msdn.microsoft.com/library/windows/hardware/ff568774)。

网络模块必须等待，直到注销都完成之前返回从其[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。

调用不需提供程序模块[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)中其[**卸载**](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 例如，在其中提供程序模块是一个复杂的驱动程序的子组件的情况下，提供程序模块注销时可能发生停用提供程序模块子组件。 但是，在这种情况下，驱动程序仍须确保，提供程序模块具有已完全取消注册从 NMR 之前从返回其**Unload**函数。

 

 





