---
title: 注册 Winsock 内核应用程序
description: 注册 Winsock 内核应用程序
ms.assetid: aaba39b8-8609-46e6-906d-3f050d91af7f
keywords:
- Winsock 内核 WDK 连接网络、 注册
- 注册 Winsock 内核应用程序
- WSK WDK 连接网络、 注册
- 网络 WSK WDK，提供程序 NPI 捕获
- 捕获 WSK NPI WDK 网络提供程序
- 客户端对象 WDK Winsock 内核
- WskRegister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d67b641949397063071d8f4e49faeb28f67abc04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391964"
---
# <a name="registering-a-winsock-kernel-application"></a>注册 Winsock 内核应用程序


### <a name="wsk-client-object-registration"></a>WSK 客户端对象注册

Winsock Kernel (WSK) 应用程序必须通过调用作为 WSK 客户端来注册[ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)函数。 **WskRegister**要求 WSK 应用程序初始化，并将指针传递到其 WSK 客户端[网络编程接口 (NPI)](network-programming-interface.md)( [ **WSK\_客户端\_NPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571163)结构) 和 WSK 注册对象 ( [ **WSK\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff571178)结构)，将由初始化**WskRegister**在成功返回。

下面的代码示例演示如何 WSK 应用程序可以将注册为 WSK 客户端。

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

WSK 应用程序不需要调用[ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)中其**DriverEntry**函数。 例如，如果 WSK 程序是一个复杂的驱动程序的子组件，激活 WSK 应用程序子组件时才，可能会出现在应用程序注册。

WSK 应用程序必须保持[ **WSK\_客户端\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571159)结构传递给**WskRegister**有效和驻留在内存中直到[ **WskDeregister** ](https://msdn.microsoft.com/library/windows/hardware/ff571128)称为和注册不再有效。 [ **WSK\_注册**](https://msdn.microsoft.com/library/windows/hardware/ff571178)结构也必须保持有效且驻留在内存中直到 WSK 应用程序停止调用的其他[WSK 注册函数](https://msdn.microsoft.com/library/windows/hardware/ff571179). 前面的代码示例中的全局数据一部分的驱动程序，从而使保持结构数据驻留在内存中卸载该驱动程序之前保留这些两个结构。

### <a name="wsk-provider-npi-capture"></a>WSK NPI 捕获提供程序

WSK 后应用程序已注册为 WSK 客户端与[ **WskRegister**](https://msdn.microsoft.com/library/windows/hardware/ff571143)，它必须使用[ **WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122)函数若要开始使用 WSK 接口捕获 WSK 提供程序 NPI WSK 子系统中。

WSK 子系统可能尚未准备就绪时不可 WSK 应用程序尝试捕获 WSK 提供程序 NPI，因为**WskCaptureProviderNPI**函数允许 WSK 应用程序轮询和 / 或等待 WSK 子系统为准备就绪如下所示：

-   如果*WaitTimeout*参数是 WSK\_否\_的等待时间，该函数将始终立即返回而不等待。

-   如果*WaitTimeout*是 WSK\_无限\_的等待时间，该函数将等待，直到 WSK 子系统变为就绪。

-   如果*WaitTimeout*是任何其他值，该函数将返回 WSK 子系统变为就绪或等待时间，以毫秒为单位，达到的值时*WaitTimeout*，以先发生者为准.

**重要**  若要避免产生负面影响的其他驱动程序和服务，WSK 调用的应用程序开始**WskCaptureProviderNPI**从其**DriverEntry**函数不应设置*WaitTimeout* WSK 参数\_无限\_等待或过长的等待时间。 此外，如果 WSK 应用程序启动很早在系统启动阶段，它应等待 WSK 子系统中比在其中一个不同的工作线程准备就绪**DriverEntry**运行。

 

如果在调用**WskCaptureProviderNPI**失败，其状态\_NOINTERFACE，WSK 应用程序可以使用[ **WskQueryProviderCharacteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff571138)若要发现 WSK 子系统所支持的范围的 WSK NPI 版本的函数。 WSK 应用程序可以调用**WskDeregister**注销其当前注册实例，并再次使用其他注册[ **WSK\_客户端\_调度** ](https://msdn.microsoft.com/library/windows/hardware/ff571159)使用受支持的 WSK NPI 版本的实例。

当**WskCaptureProviderNPI**成功，返回其*WskProviderNpi*参数指向 WSK 提供程序 NPI ( [ **WSK\_提供程序\_NPI**](https://msdn.microsoft.com/library/windows/hardware/ff571177)) 准备就绪可供 WSK 应用程序。 WSK\_提供程序\_NPI 结构包含 WSK 客户端对象的指针 ( [ **WSK\_客户端**](https://msdn.microsoft.com/library/windows/hardware/ff571155)) 和[ **WSK\_提供程序\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571175) WSK 应用程序可用于创建 WSK 套接字并执行其他操作 WSK 客户端对象上的 WSK 函数调度表。 后 WSK 应用程序已完成使用 WSK\_提供程序\_调度的函数，它必须通过调用释放 WSK 提供程序 NPI [ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)。

下面的代码示例显示了 WSK 应用程序可以捕获 WSK 提供程序 NPI、 使用它来创建套接字时，，然后将其释放。

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

WSK 应用程序可以调用[ **WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122)不止一次。 每次调用**WskCaptureProviderNPI**成功返回，必须相应地调用[ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)。 WSK 应用程序必须不执行任何进一步调用到中的函数[ **WSK\_提供程序\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571175)后调用**WskReleaseProviderNPI**.

 

 





