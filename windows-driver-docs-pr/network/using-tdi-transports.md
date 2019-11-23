---
title: 使用 TDI 传输
description: 使用 TDI 传输
ms.assetid: 58fb5e62-e15d-4f15-8eb3-3e302ea08c4f
keywords:
- TDI 传输 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb4f82a3bc0315636a9172092a2579f31f05e73c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842972"
---
# <a name="using-tdi-transports"></a>使用 TDI 传输


Winsock 内核（WSK）子系统为使用[TDI](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565094(v=vs.85))传输提供支持。 为了通过 WSK[网络编程接口（NPI）](network-programming-interface.md)使用 TDI 传输，WSK 应用程序必须将每个 tdi 传输所使用的每个 tdi 传输的地址族、套接字类型和协议的组合映射到每个 tdi 传输的关联设备名称。 WSK 应用程序使用[**WSK\_tdi\_DEVICENAME\_映射**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-tdi-devicename-mapping)客户端控制操作，将地址族、套接字类型和协议的组合映射到 TDI 传输的设备名称。

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

**请注意**，在 Windows Vista 之后的 Microsoft windows 版本中不支持  TDI。 请改用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 

 





