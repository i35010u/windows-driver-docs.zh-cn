---
title: 使用 TDI 传输
description: 使用 TDI 传输
ms.assetid: 58fb5e62-e15d-4f15-8eb3-3e302ea08c4f
keywords:
- TDI 传输 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7aea86c48ef59b0164d016b3983e5e41b4a1c75
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205925"
---
# <a name="using-tdi-transports"></a>使用 TDI 传输


Winsock 内核 (WSK) 子系统为使用 [TDI](/previous-versions/windows/hardware/network/ff565094(v=vs.85)) 传输提供支持。 为了通过 WSK [网络编程接口 (NPI) ](network-programming-interface.md)使用 TDI 传输，WSK 应用程序必须将每个 tdi 传输所使用的每个 tdi 传输的地址族、套接字类型和协议的组合映射到每个 tdi 传输的关联设备名称。 WSK 应用程序使用 [**WSK \_ TDI \_ DEVICENAME \_ 映射**](./wsk-tdi-devicename-mapping.md) 客户端控制操作，将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称。

下面的代码示例演示 WSK 应用程序如何将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称。

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

WSK 应用程序必须先将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称，然后再创建任何套接字。 在 WSK 应用程序成功将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称后，应用程序就可以创建使用映射的 TDI 传输的新套接字。

**注意**   Windows Vista 之后的 Microsoft Windows 版本不支持 TDI。 请改用 [Windows 筛选平台](/windows-hardware/drivers/ddi/_netvista/) 或 [Winsock 内核](/windows-hardware/drivers/ddi/_netvista/) 。

 

 

