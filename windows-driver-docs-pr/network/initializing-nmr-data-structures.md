---
title: 初始化 NMR 数据结构
description: 初始化 NMR 数据结构
ms.assetid: 84241ff4-f6ae-4c71-a9e3-1a6615e41293
keywords:
- 网络模块注册机构 WDK Winsock 内核
- NMR WDK Winsock 内核
- 初始化 NMR 数据结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 122baf2c7a0fd8cc805be592a803fa9944c77478
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546749"
---
# <a name="initializing-nmr-data-structures"></a>初始化 NMR 数据结构


应用程序可以使用注册之前 Winsock Kernel (WSK)[网络模块注册机构 (NMR)](network-module-registrar2.md)，应用程序必须首先初始化以下结构。

-   [**NPI\_MODULEID**](https://msdn.microsoft.com/library/windows/hardware/ff568813)

-   [**NPI\_客户端\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff568812)

-   [**NPI\_注册\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff568815)中包含[ **NPI\_客户端\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff568812)结构

只要 WSK 应用程序已注册 NMR，所有这些数据结构必须保持有效且驻留在内存中。

下面的代码示例显示了 WSK 应用程序可以初始化所有前面列出的数据结构。

```C++
// Include the WSK header file
#include "wsk.h"

// Structure for the WSK application&#39;s network module identification
const NPI_MODULEID ModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the WSK application
};

// Prototypes for the WSK application&#39;s NMR API callback functions
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

// Structure for the WSK application&#39;s characteristics
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

WSK 应用程序调用[ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)函数向 NMR 注册应用程序。

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

WSK 应用程序不需要调用**NmrRegisterClient**从其**DriverEntry**函数。 例如，如果 WSK 程序是一个复杂的驱动程序的子组件，激活 WSK 应用程序子组件时才，可能会出现在应用程序注册。

 

 





