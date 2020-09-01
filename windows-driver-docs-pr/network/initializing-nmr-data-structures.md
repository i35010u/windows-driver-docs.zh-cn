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
ms.openlocfilehash: 53a4110983addd5e5a61d5e5f13ed9904722cb52
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211043"
---
# <a name="initializing-nmr-data-structures"></a>初始化 NMR 数据结构


在使用 Winsock 内核 (WSK) 应用程序可以向 [网络模块注册器 (NMR) ](network-module-registrar2.md)注册后，应用程序必须先初始化以下结构。

-   [**NPI \_ MODULEID**](/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))

-   [**NPI \_ 客户端 \_ 特征**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)

-   [**NPI \_\_**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance) [**NPI \_ 客户端 \_ 特征**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)结构中包含的注册实例

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

WSK 应用程序调用 [**NmrRegisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 函数来向 NMR 注册应用程序。

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

 

