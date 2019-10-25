---
title: 针对客户端对象执行控制操作
description: 针对客户端对象执行控制操作
ms.assetid: 080c4821-43ea-4b6d-a55a-99621db17fb7
keywords:
- Winsock 内核 WDK 网络，控制操作
- WSK WDK 网络，控制操作
- 控制操作 WDK Winsock 内核
- 客户端对象 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680527a1ef9a0054e84fc73312f5a62ea1bb3a62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843690"
---
# <a name="performing-control-operations-on-a-client-object"></a>针对客户端对象执行控制操作


Winsock 内核（WSK）应用程序成功附加到 WSK 子系统后，它可以在附件期间 WSK 子系统返回的客户端对象（ [**WSK\_客户端**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)）上执行控制操作。 这些控件操作不特定于特定的套接字，而是具有更通用的作用域。 有关可对客户端对象执行的每个控件操作的详细信息，请参阅[WSK Client Control 操作](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client-control-operations)。

WSK 应用程序通过调用[**WskControlClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_client)函数来执行客户端控件操作。 **WskControlClient**函数由[**WSK\_提供\_程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)的**WskControlClient**成员指向，WSK 子系统在附件期间返回的调度结构。

下面的代码示例演示 WSK 应用程序如何使用[**WSK\_传输\_列表\_查询**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-transport-list-query)客户端控制操作来检索可在创建新套接字时指定的可用网络传输的列表。

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

 

 





