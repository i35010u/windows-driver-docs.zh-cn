---
title: 卸载客户端模块
description: 卸载客户端模块
ms.assetid: 2cca2918-ce0b-4016-b3f2-fbbc06c0b7f7
keywords:
- 客户端模块 WDK 网络模块注册机构，卸载
- 正在卸载的网络模块
- NmrDeregisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f79248bd77e9a5170b083da4d30ff0e98ee603e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346635"
---
# <a name="unloading-a-client-module"></a>卸载客户端模块


若要卸载客户端模块，操作系统将调用客户端模块[**卸载**](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 请参阅[初始化和注册客户端模块](initializing-and-registering-a-client-module.md)有关如何指定客户端模块的详细信息**卸载**在初始化过程中的函数。

客户端模块[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数还可确保从系统内存中卸载客户端模块之前，以此客户端模块从网络模块注册机构 (NMR)。 客户端模块启动注销 NMR 从通过调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)函数，它通常会调用从其**卸载**函数。 客户端模块不能返回从其**Unload**后它具有已完全取消注册从 NMR 直到正常。 如果在调用**NmrDeregisterClient**将返回状态\_挂起状态，必须调用客户端模块[ **NmrWaitForClientDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568786)函数等待注销完成之前它将返回其**Unload**函数。

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

如果客户端模块已注册为多个客户端[网络编程接口 (NPIs)](network-programming-interface.md)，它必须调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)为它支持每个 NPI。 如果网络模块已注册为客户端模块和提供程序模块 （也就是说，它是一个 NPI 的客户端和提供程序的另一个 NPI），它必须同时调用**NmrDeregisterClient**并[ **NmrDeregisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff568778)。

网络模块必须等待，直到注销都完成之前返回从其[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。

客户端模块不需要调用[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)中其[**卸载**](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 例如，在其中客户端模块是一个复杂的驱动程序的子组件的情况下，客户端模块注销时可能发生的客户端模块子组件将停用。 但是，在这种情况下，驱动程序仍须确保，客户端模块具有已完全取消注册从 NMR 之前从返回其**Unload**函数。

 

 





