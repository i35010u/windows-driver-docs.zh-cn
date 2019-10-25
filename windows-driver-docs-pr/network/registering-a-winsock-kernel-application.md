---
title: 注册 Winsock 内核应用程序
description: 注册 Winsock 内核应用程序
ms.assetid: aaba39b8-8609-46e6-906d-3f050d91af7f
keywords:
- Winsock 内核 WDK 网络，注册
- 注册 Winsock 内核应用程序
- WSK WDK 网络，注册
- WSK WDK 网络，提供程序 NPI 捕获
- 捕获 WSK 提供程序 NPI WDK 网络
- 客户端对象 WDK Winsock 内核
- WskRegister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 425fa6f0a8f5d6936d696ecb198dfe40227c83d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842096"
---
# <a name="registering-a-winsock-kernel-application"></a>注册 Winsock 内核应用程序


### <a name="wsk-client-object-registration"></a>WSK 客户端对象注册

Winsock 内核（WSK）应用程序必须通过调用[**WskRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)函数注册为 WSK 客户端。 **WskRegister**要求 WSK 应用程序进行初始化，并将指针传递到其 WSK 客户端的[网络编程接口（NPI）](network-programming-interface.md)（ [**WSK\_客户端\_NPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_npi)结构）和 WSK 注册对象（ [**WSK\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration)结构），该结构将在成功返回时通过**WskRegister**进行初始化。

下面的代码示例演示 WSK 应用程序如何注册为 WSK 客户端。

```C++
// Include the WSK header file
#include "wsk.h"

// WSK Client Dispatch table that denotes the WSK version
// that the WSK application wants to use and optionally a pointer
// to the WskClientEvent callback function
const WSK_CLIENT_DISPATCH WskAppDispatch = {
  MAKE_WSK_VERSION(1,0), // Use WSK version 1.0
  0,    // Reserved
  NULL  // WskClientEvent callback not required for WSK version 1.0
};

// WSK Registration object
WSK_REGISTRATION WskRegistration;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;
  WSK_CLIENT_NPI wskClientNpi;

  .
  . 
  .

  // Register the WSK application
  wskClientNpi.ClientContext = NULL;
  wskClientNpi.Dispatch = &WskAppDispatch;
  Status = WskRegister(&wskClientNpi, &WskRegistration);

  if(!NT_SUCCESS(Status)) {
      .
      .
      .
      return Status;
  }

  .
  . 
  .
}
```

WSK 应用程序不需要从其**DriverEntry**函数内调用[**WskRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则仅当激活 WSK 应用程序子组件时，应用程序的注册才可能发生。

WSK 应用程序必须将传递给 WskRegister 的[**WSK\_客户端\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)结构传递到，并将其传递给 ，直到调用[**WskDeregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)并且注册不再有效。 [**WSK\_注册**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration)结构还必须保持有效，并驻留在内存中，直到 WSK 应用程序停止调用其他[WSK 注册函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。 前面的代码示例在驱动程序的 "全局数据" 部分中保留这两个结构，从而在卸载驱动程序之前将结构数据保存在内存中。

### <a name="wsk-provider-npi-capture"></a>WSK 提供程序 NPI 捕获

将 WSK 应用程序注册为具有[**WskRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)的 WSK 客户端之后，它必须使用[**WSKCAPTUREPROVIDERNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)函数从 WSK 子系统捕获 NPI 提供程序 WSK，才能开始使用 WSK 接口。

因为当 WSK 应用程序尝试捕获 WSK 提供程序 NPI 时，WSK 子系统可能尚未准备好， **WskCaptureProviderNPI**函数允许 WSK 应用程序轮询或等待 WSK 子系统变为就绪，如下所示：

-   如果*WaitTimeout*参数为 WSK\_\_等待，则该函数将始终立即返回而不等待。

-   如果*WaitTimeout*为 WSK\_无限\_等待，则该函数将等待，直到 WSK 子系统准备就绪。

-   如果*WaitTimeout*为其他任何值，则当 WSK 子系统准备就绪或等待时间（以毫秒为单位）到达*WaitTimeout*的值（以先发生的时间为准）时，函数将返回。

**重要**  为了避免对其他驱动程序和服务的启动产生不利影响，从其**DriverEntry**函数调用**WskCaptureProviderNPI**的 WSK 应用程序不应将*WaitTimeout*参数设置为 WSK\_无限\_等待或过长的等待时间。 此外，如果 WSK 应用程序在系统启动阶段的早期启动，则应等待 WSK 子系统在不同的工作线程中准备就绪，而不是**DriverEntry**运行的工作线程。

 

如果对**WskCaptureProviderNPI**的调用失败，状态\_NOINTERFACE，则 WSK 应用程序可以使用[**WskQueryProviderCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskqueryprovidercharacteristics)函数来发现 WSK 子系统支持的 NPI WSK 版本的范围。 WSK 应用程序可以调用**WskDeregister**来取消注册其当前注册实例，然后使用不同的[**WSK\_客户端\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)使用受支持 WSK NPI 版本的调度实例再次注册。

当**WskCaptureProviderNPI**成功返回时，其*WskProviderNpi*参数将指向 WSK 提供程序 NPI （ [**WSK\_提供程序\_NPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_npi)），供 WSK 应用程序使用。 NPI 结构中的 WSK\_提供\_程序包含指向 WSK 客户端对象（ [**WSK\_客户端**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)）的指针\_，以及 WSK 应用程序可用于创建的 WSK 函数[ **\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)调度表WSK 套接字，并对 WSK 客户端对象执行其他操作。 使用 WSK\_提供程序\_调度函数完成 WSK 应用程序后，必须通过调用[**WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)释放 WSK 提供程序 NPI。

下面的代码示例演示 WSK 应用程序如何捕获 WSK 提供程序 NPI，如何使用它来创建套接字，然后将其释放。

```C++
// WSK application routine that waits for WSK subsystem
// to become ready and captures the WSK Provider NPI
NTSTATUS
  WskAppWorkerRoutine(
    )
{
  NTSTATUS Status;
  WSK_PROVIDER_NPI wskProviderNpi;
 
  // Capture the WSK Provider NPI. If WSK subsystem is not ready yet,
  // wait until it becomes ready.
  Status = WskCaptureProviderNPI(
    &WskRegistration, // must have been initialized with WskRegister
    WSK_INFINITE_WAIT,
    &wskProviderNpi
    );

  if(!NT_SUCCESS(Status))
  {
    // The WSK Provider NPI could not be captured.
    if( Status == STATUS_NOINTERFACE ) {
      // WSK application's requested version is not supported
    }
    else if( status == STATUS_DEVICE_NOT_READY ) {
      // WskDeregister was invoked in another thread thereby causing
      // WskCaptureProviderNPI to be canceled.
    } 
    else {
      // Some other unexpected failure has occurred
    }

    return Status;
  }

  // The WSK Provider NPI has been captured.
  // Create and set up a listening socket that accepts
   // incoming connections.
  Status = CreateListeningSocket(&wskProviderNpi, ...);

  // The WSK Provider NPI will not be used any more.
  // So, release it here immediately.
  WskReleaseProviderNPI(&WskRegistration);

  // Return result of socket creation routine
  return Status;

}
```

WSK 应用程序可以多次调用[**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi) 。 对于成功返回的**WskCaptureProviderNPI**的每个调用，必须对[**WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)进行相应的调用。 调用**WskReleaseProviderNPI**后，WSK 应用程序不能对[**WSK\_提供\_程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)中的函数进行任何进一步调用。

 

 





