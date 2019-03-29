---
title: 初始化和注册提供程序模块
description: 初始化和注册提供程序模块
ms.assetid: 967271ce-e4f5-45ce-9249-746d2fe698c1
keywords:
- 提供程序模块 WDK 网络模块注册机构，初始化
- 提供程序模块 WDK 网络模块注册机构，注册
- 正在注册模块提供程序
- 初始化提供程序的模块
- NmrRegisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 008f31c858d04c81bdc2cc3e7f3508a293528cc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568305"
---
# <a name="initializing-and-registering-a-provider-module"></a>初始化和注册提供程序模块


提供程序模块必须先它可以注册其自身与网络模块注册机构 (NMR) 初始化数据结构的数。 这些结构包括[ **NPI\_MODULEID** ](https://msdn.microsoft.com/library/windows/hardware/ff568813)结构[ **NPI\_提供程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff568814)结构[ **NPI\_注册\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff568815)结构 (包含在 NPI\_提供程序\_特征结构），并由提供程序模块的注册上下文使用的提供程序模块定义的结构。

如果提供程序模块向注册自身 NMR 作为提供商[网络编程接口 (NPI)](network-programming-interface.md) ，用于定义特定于 NPI 的提供程序特征、 提供程序模块还必须初始化提供程序实例特性结构，它由 NPI 定义。

所有这些数据结构必须保持有效且驻留在内存中，只要向 NMR 注册提供程序模块。

例如，假设"EXNPI"NPI 标头文件 Exnpi.h 中定义了以下：

```C++
// EXNPI NPI identifier
const NPIID EXNPI_NPIID = { ... };

// EXNPI provider characteristics structure
typedef struct EXNPI_PROVIDER_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_PROVIDER_CHARACTERISTICS, *PEXNPI_PROVIDER_CHARACTERISTICS;
```

下面显示了如何将自身注册为 EXNPI NPI 的提供程序的提供程序模块可以初始化所有这些数据结构：

```C++
// Include the NPI specific header file
#include "exnpi.h"

// Structure for the provider module's NPI-specific characteristics
const EXNPI_PROVIDER_CHARACTERISTICS NpiSpecificCharacteristics =
{
  .
  . // The NPI-specific characteristics of the provider module
  .
};

// Structure for the provider module's identification
const NPI_MODULEID ProviderModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the provider module
};

// Prototypes for the provider module's callback functions
NTSTATUS
  ProviderAttachClient(
    IN HANDLE NmrBindingHandle,
    IN PVOID ProviderContext,
    IN PNPI_REGISTRATION_INSTANCE ClientRegistrationInstance,
    IN PVOID ClientBindingContext,
    IN CONST VOID *ClientDispatch,
    OUT PVOID *ProviderBindingContext,
    OUT PVOID *ProviderDispatch
    );

NTSTATUS
  ProviderDetachClient(
    IN PVOID ProviderBindingContext
    );

VOID
  ProviderCleanupBindingContext(
    IN PVOID ProviderBindingContext
    );

// Structure for the provider module's characteristics
const NPI_PROVIDER_CHARACTERISTICS ProviderCharacteristics =
{
  0,
  sizeof(NPI_PROVIDER_CHARACTERISTICS),
  ProviderAttachClient,
  ProviderDetachClient,
  ProviderCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &EXNPI_NPIID,
    &ProviderModuleId,
    0,
    &NpiSpecificCharacteristics
  }
};

// Context structure for the provider module's registration
typedef struct PROVIDER_REGISTRATION_CONTEXT_ {
  .
  . // Provider-specific members
  .
} PROVIDER_REGISTRATION_CONTEXT, *PPROVIDER_REGISTRATION_CONTEXT;

// Structure for the provider's registration context
PROVIDER_REGISTRATION_CONTEXT ProviderRegistrationContext =
{
  .
  . // Initial values for the registration context
  .
};
```

提供程序模块通常初始化单独存在于其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 提供程序模块的主要初始化任务包括：

-   指定[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 当提供程序模块是从系统中卸载时，操作系统将调用此函数。 如果提供程序模块不提供卸载函数，该提供程序模块不能为从系统中卸载。

-   调用[ **NmrRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568784) NMR 向注册提供程序模块的函数。

例如：

```C++
// Prototype for the provider module's unload function
VOID
  Unload(
    PDRIVER_OBJECT DriverObject
   );

// Variable to contain the handle for the registration
HANDLE ProviderHandle;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;

  // Specify the unload function
  DriverObject->DriverUnload = Unload;

  .
  . // Other initialization tasks
  .

  // Register the provider module with the NMR
  Status = NmrRegisterProvider(
    &ProviderCharacteristics,
    &ProviderRegistrationContext,
    &ProviderHandle
    );

  // Return the result of the registration
  return Status;
}
```

如果提供程序模块的多个 NPI 提供程序，它必须初始化一组独立的数据结构，并调用[ **NmrRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568784)为它支持每个 NPI。 如果网络模块是提供程序模块和客户端模块 （也就是说，它是一个 NPI 的提供程序和客户端的另一个 NPI），它必须初始化两个独立的数据结构，提供程序接口和客户端接口集并同时调用**NmrRegisterProvider**并[ **NmrRegisterClient**](https://msdn.microsoft.com/library/windows/hardware/ff568782)。

调用不需提供程序模块[ **NmrRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568784)中其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 例如，在其中提供程序模块是一个复杂的驱动程序的子组件的情况下，提供程序模块的注册时可能发生仅激活提供程序模块子组件。

有关实现提供程序模块的详细信息[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数中，请参阅[卸载提供程序模块](unloading-a-provider-module.md)。

 

 





