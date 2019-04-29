---
title: 针对客户端对象执行控制操作
description: 针对客户端对象执行控制操作
ms.assetid: 080c4821-43ea-4b6d-a55a-99621db17fb7
keywords:
- 网络、 Winsock 内核 WDK 控制操作
- WSK WDK 网络、 控制操作
- 控制操作 WDK Winsock 内核
- 客户端对象 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c33669d826048428025bfc781d1040ad37c3d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372219"
---
# <a name="performing-control-operations-on-a-client-object"></a>针对客户端对象执行控制操作


Winsock Kernel (WSK) 应用程序已成功附加到 WSK 子系统之后，它可以执行客户端对象上的控制操作 ( [ **WSK\_客户端**](https://msdn.microsoft.com/library/windows/hardware/ff571155)) 返回在附件 WSK 子系统。 这些控制操作不是特定于特定的套接字，但改为具有更多常规的作用域。 有关每个可在客户端对象执行管理操作的详细信息，请参阅[WSK 客户端控制操作](https://msdn.microsoft.com/library/windows/hardware/ff571157)。

WSK 应用程序通过调用执行客户端管理操作[ **WskControlClient** ](https://msdn.microsoft.com/library/windows/hardware/ff571126)函数。 **WskControlClient**函数所指向的**WskControlClient**的成员[ **WSK\_提供程序\_调度**](https://msdn.microsoft.com/library/windows/hardware/ff571175)期间附件 WSK 子系统返回的结构。

下面的代码示例演示如何使用一个应用程序，WSK [ **WSK\_传输\_列表\_查询**](https://msdn.microsoft.com/library/windows/hardware/ff571195)客户端管理操作来检索的列表创建新的套接字时，可以指定可用的网络传输。

```C++
// Function to retrieve a list of available network transports
NTSTATUS
  GetTransportList(
    PWSK_PROVIDER_NPI WskProviderNpi,
    PWSK_TRANSPORT TransportList,
    ULONG MaxTransports,
    PULONG TransportsRetrieved
    )
{
  SIZE_T BytesRetrieved;
  NTSTATUS Status;

  // Perform client control operation
  Status =
    WskProviderNpi->Dispatch->
        WskControlClient(
          WskProviderNpi->Client,
          WSK_TRANSPORT_LIST_QUERY,
          0,
          NULL,
          MaxTransports * sizeof(WSK_TRANSPORT),
          TransportList,
          &BytesRetrieved,
          NULL  // No IRP for this control operation
          );

  // Convert bytes retrieved to transports retrieved
  TransportsRetrieved = BytesRetrieved / sizeof(WSK_TRANSPORT);

  // Return status of client control operation
  return Status;
}
```

 

 





