---
title: 卸载客户端模块
description: 卸载客户端模块
keywords:
- 客户端模块 WDK 网络模块注册器，卸载
- 卸载网络模块
- NmrDeregisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a74b9cf05a13af05eaee5f6d10db7c092fcfe3a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839423"
---
# <a name="unloading-a-client-module"></a>卸载客户端模块


若要卸载客户端模块，操作系统将调用客户端模块的 [**unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数。 有关如何在初始化过程中指定客户端模块的 **Unload** 函数的详细信息，请参阅 [初始化和注册客户端模块](initializing-and-registering-a-client-module.md)。

客户端模块的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数可确保从系统内存中卸载客户端模块之前，从网络模块注册器 (NMR) 取消注册客户端模块。 客户端模块通过调用 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient) 函数开始从 NMR 注销，该函数通常从其 **Unload** 函数调用它。 在从 NMR 完全取消注册后，客户端模块不能从其 **Unload** 函数返回。 如果对 **NmrDeregisterClient** 的调用返回状态 " \_ 挂起"，则客户端模块必须调用 [**NmrWaitForClientDeregisterComplete**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforclientderegistercomplete) 函数以等待注销完成，然后再从其 **Unload** 函数返回。

例如：

```C++
// Variable containing the handle for the registration
HANDLE ClientHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Deregister the client module from the NMR
  Status =
    NmrDeregisterClient(
      ClientHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the deregistration to be completed
    NmrWaitForClientDeregisterComplete(
      ClientHandle
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

如果客户端模块注册为多个 [网络编程接口的客户端 (NPIs)](network-programming-interface.md)，则它必须为它支持的每个 NPI 调用 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient) 。 如果将网络模块注册为客户端模块和提供程序模块 (也就是说，它是一个 NPI 的客户端和另一个 NPI) 的提供程序，则它必须同时调用 **NmrDeregisterClient** 和 [**NmrDeregisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)。

在从其 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数返回之前，网络模块必须一直等待，直到所有注销都完成。

不需要客户端模块从其 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数中调用 [**NmrDeregisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient) 。 例如，在客户端模块是复杂驱动程序的子组件的情况下，当停用客户端模块子组件时，可能会取消注册客户端模块。 但是，在这种情况下，驱动程序必须确保在从 NMR 的 **Unload** 函数返回之前已完全从取消对该客户端模块的注册。

 

