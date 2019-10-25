---
title: 初始化 NMR 数据结构
description: 初始化 NMR 数据结构
ms.assetid: 84241ff4-f6ae-4c71-a9e3-1a6615e41293
keywords:
- 网络模块注册器 WDK Winsock 内核
- NMR WDK Winsock 内核
- 初始化 NMR 数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c58da13ba5823fe2dcb55ad41cc0dbbb83b55fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824416"
---
# <a name="initializing-nmr-data-structures"></a>初始化 NMR 数据结构


在 Winsock 内核（WSK）应用程序可以注册到[网络模块注册机构（NMR）](network-module-registrar2.md)之前，应用程序必须先初始化以下结构。

-   [**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))

-   [**NPI\_客户端\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)

-   [**NPI\_注册\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)包含在[**NPI\_客户端\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)结构内的实例

只要向 NMR 注册了 WSK 应用程序，所有这些数据结构都必须保持有效并驻留在内存中。

下面的代码示例演示 WSK 应用程序如何初始化前面列出的所有数据结构。

```C++
// Include the WSK header file
#include "wsk.h"

// Structure for the WSK application's network module identification
const NPI_MODULEID ModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the WSK application
};

// Prototypes for the WSK application's NMR API callback functions
NTSTATUS
  ClientAttachProvider(
    IN HANDLE NmrBindingHandle,
    IN PVOID ClientContext,
    IN PNPI_REGISTRATION_INSTANCE ProviderRegistrationInstance
    );

NTSTATUS
  ClientDetachProvider(
    IN PVOID ClientBindingContext
    );

VOID
  ClientCleanupBindingContext(
    IN PVOID ClientBindingContext
    );

// Structure for the WSK application's characteristics
const NPI_CLIENT_CHARACTERISTICS Characteristics =
{
  0,
  sizeof(NPI_CLIENT_CHARACTERISTICS),
  ClientAttachProvider,
  ClientDetachProvider,
  ClientCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &NPI_WSK_INTERFACE_ID,
    &ModuleId,
    0,
    NULL
  }
};
```

WSK 应用程序调用[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)函数来向 NMR 注册应用程序。

例如：

```C++
// Variable to contain the handle for the registration with the NMR
HANDLE RegistrationHandle;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;

  .
  .
  .

  // Register the WSK application with the NMR
  Status = NmrRegisterClient(
    &Characteristics,
    NULL,
    &RegistrationHandle
    );

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

WSK 应用程序不需要从其**DriverEntry**函数内调用**NmrRegisterClient** 。 例如，如果 WSK 应用程序是复杂驱动程序的子组件，则仅当激活 WSK 应用程序子组件时，应用程序的注册才可能发生。

 

 





