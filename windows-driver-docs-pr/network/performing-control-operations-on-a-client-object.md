---
title: 针对客户端对象执行控制操作
description: 针对客户端对象执行控制操作
keywords:
- Winsock 内核 WDK 网络，控制操作
- WSK WDK 网络，控制操作
- 控制操作 WDK Winsock 内核
- 客户端对象 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f06bf605143e2e565c72b976b2002e269e463f77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809919"
---
# <a name="performing-control-operations-on-a-client-object"></a>针对客户端对象执行控制操作


Winsock 内核 (WSK) 应用程序已成功连接到 WSK 子系统后，它可以对客户端对象执行控制操作， ( [**WSK \_ 客户端**](./wsk-client.md)) ，在附件期间 WSK 子系统返回。 这些控件操作不特定于特定的套接字，而是具有更通用的作用域。 有关可对客户端对象执行的每个控件操作的详细信息，请参阅 [WSK Client Control 操作](wsk-cache-sd.md)。

WSK 应用程序通过调用 [**WskControlClient**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client) 函数来执行客户端控件操作。 **WskControlClient** 函数由 WSK 子系统在附件期间返回的 [**WSK \_ 提供程序 \_ 调度**](/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)结构的 **WskControlClient** 成员指向。

下面的代码示例演示 WSK 应用程序如何使用 [**WSK \_ 传输 \_ 列表 \_ 查询**](./wsk-transport-list-query.md) 客户端控制操作来检索可在创建新套接字时指定的可用网络传输的列表。

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

 

