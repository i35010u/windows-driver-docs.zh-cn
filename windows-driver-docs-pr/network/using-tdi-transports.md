---
title: 使用 TDI 传输
description: 使用 TDI 传输
ms.assetid: 58fb5e62-e15d-4f15-8eb3-3e302ea08c4f
keywords:
- TDI 传输 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2753f2b49cde398da3caba407475f72b60dc9cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372480"
---
# <a name="using-tdi-transports"></a>使用 TDI 传输


Winsock Kernel (WSK) 子系统提供了支持使用[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))传输。 若要使用 TDI 传输通过 WSK[网络编程接口 (NPI)](network-programming-interface.md)、 WSK 应用程序必须映射的地址族，套接字类型组合，并且为每个 TDI 的协议传输它使用为关联的设备名称每个这些 TDI 传输。 WSK 应用程序映射的地址族，套接字类型，组合和使用传输协议与设备名称的 TDI [ **WSK\_TDI\_DEVICENAME\_映射**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-tdi-devicename-mapping)客户端管理操作。

下面的代码示例显示如何 WSK 应用程序可以映射的地址族、 套接字类型和协议组合与 TDI 传输的设备名称。

```C++
// Number of TDI mappings
#define MAPCOUNT 2

// Array of TDI mappings
const WSK_TDI_MAP TdiMap[MAPCOUNT] =
{
  {SOCK_STREAM, ..., ..., ...},
  {SOCK_DGRAM, ..., ..., ...}
};

// TDI map info structure
const WSK_TDI_MAP_INFO TdiMapInfo =
{
  MAPCOUNT,
  TdiMap
}

// Function to set the TDI map
NTSTATUS
  SetTdiMap(
    PWSK_APP_BINDING_CONTEXT BindingContext
  )
{
  NTSTATUS Status;

  // Perform client control operation
  Status =
    BindingContext->
      WskProviderDispatch->
        WskControlClient(
          BindingContext->WskClient,
          WSK_TDI_DEVICENAME_MAPPING,
          sizeof(WSK_TDI_MAP_INFO),
          &TdiMapInfo,
          0,
          NULL,
          NULL,
          NULL  // No IRP for this control operation
          );

  // Return status of client control operation
  return Status;
}
```

WSK 应用程序必须映射到 TDI 传输的设备名称的地址族、 套接字类型和协议组合，它会创建任何套接字之前。 WSK 应用程序已成功映射的地址族、 套接字类型和协议组合到 TDI 传输的设备名称后，应用程序可以创建新的套接字使用的映射的 TDI 传输。

**请注意**  TDI 将不支持在 Microsoft Windows 版本在 Windows Vista 后。 使用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)相反。

 

 

 





