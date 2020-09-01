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
ms.openlocfilehash: 55de4ebfead80c9e9e46f55a32cc8f85a95d9822
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212047"
---
# <a name="registering-a-winsock-kernel-application"></a>注册 Winsock 内核应用程序


### <a name="wsk-client-object-registration"></a>WSK 客户端对象注册

Winsock 内核 (WSK) 应用程序必须通过调用 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 函数注册为 WSK 客户端。 **WskRegister** 要求 WSK 应用程序进行初始化，并将指针传递到其 WSK 客户端的 [网络编程接口 (NPI) ](network-programming-interface.md) ([**WSK \_ 客户端 \_ NPI**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_npi) 结构) 和 WSK 注册对象 ([**WSK \_ 注册**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration) 结构) 将在成功返回时由 **WskRegister** 初始化。

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

WSK 应用程序不需要从其**DriverEntry**函数内调用[**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则仅当激活 WSK 应用程序子组件时，应用程序的注册才可能发生。

WSK 应用程序必须保持传递给**WskRegister**的[**WSK \_ 客户端 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)结构有效并驻留在内存中，直到调用[**WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)并且注册不再有效。 [**WSK \_ 注册**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration)结构还必须保持有效，并驻留在内存中，直到 WSK 应用程序停止调用其他[WSK 注册函数](/windows-hardware/drivers/ddi/_netvista/)。 前面的代码示例在驱动程序的 "全局数据" 部分中保留这两个结构，从而在卸载驱动程序之前将结构数据保存在内存中。

### <a name="wsk-provider-npi-capture"></a>WSK 提供程序 NPI 捕获

将 WSK 应用程序注册为具有 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)的 WSK 客户端之后，它必须使用 [**WSKCAPTUREPROVIDERNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi) 函数从 WSK 子系统捕获 NPI 提供程序 WSK，才能开始使用 WSK 接口。

因为当 WSK 应用程序尝试捕获 WSK 提供程序 NPI 时，WSK 子系统可能尚未准备好， **WskCaptureProviderNPI** 函数允许 WSK 应用程序轮询或等待 WSK 子系统变为就绪，如下所示：

-   如果 *WaitTimeout* 参数为 WSK \_ NO \_ WAIT，则该函数将始终立即返回而不等待。

-   如果 *WaitTimeout* 为 WSK \_ 无限 \_ 等待，则函数将等待，直到 WSK 子系统准备就绪。

-   如果 *WaitTimeout* 为其他任何值，则当 WSK 子系统准备就绪或等待时间（以毫秒为单位）到达 *WaitTimeout*的值（以先发生的时间为准）时，函数将返回。

**重要提示**   为了避免对其他驱动程序和服务的启动产生不利影响，从其**DriverEntry**函数调用**WskCaptureProviderNPI**的 WSK 应用程序不应将*WaitTimeout*参数设置为 WSK \_ 无限 \_ 等待或过长的等待时间。 此外，如果 WSK 应用程序在系统启动阶段的早期启动，则应等待 WSK 子系统在不同的工作线程中准备就绪，而不是 **DriverEntry** 运行的工作线程。

 

如果对 **WskCaptureProviderNPI** 的调用失败，状态为 \_ NOINTERFACE，则 WSK 应用程序可以使用 [**WSKQUERYPROVIDERCHARACTERISTICS**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskqueryprovidercharacteristics) 函数来发现 WSK 子系统支持的 NPI WSK 版本的范围。 WSK 应用程序可以调用 **WskDeregister** 来注销其当前注册实例，然后使用不同的 [**WSK \_ 客户端 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch) 实例再次注册，该实例使用受支持的 WSK NPI 版本。

当 **WskCaptureProviderNPI** 成功返回时，其 *WSKPROVIDERNPI* 参数指向 WSK 提供程序 NPI ( [**WSK \_ 提供程序 \_ NPI**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_npi)) 可供 WSK 应用程序使用。 WSK \_ PROVIDER \_ NPI 结构包含指向 WSK 客户端对象 ( [**WSK \_ 客户**](./wsk-client.md) 端) 和 WSK [**提供程序 \_ \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch) 调度表的指针，WSK 应用程序可使用这些函数创建 WSK 套接字并对 WSK 客户端对象执行其他操作。 使用 WSK 提供程序调度函数完成 WSK 应用程序后 \_ \_ ，必须通过调用 [**WskReleaseProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)释放 WSK 提供程序 NPI。

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

WSK 应用程序可以多次调用 [**WskCaptureProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi) 。 对于成功返回的 **WskCaptureProviderNPI** 的每个调用，必须对 [**WskReleaseProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)进行相应的调用。 在调用**WskReleaseProviderNPI**后，WSK 应用程序不能对[**WSK \_ 提供程序 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)中的函数进行进一步调用。

 

