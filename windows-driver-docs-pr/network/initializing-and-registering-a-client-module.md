---
title: 初始化和注册客户端模块
description: 初始化和注册客户端模块
ms.assetid: 3d0941d0-5a6f-4c6d-b519-af850a8de341
keywords:
- 客户端模块 WDK 网络模块注册机构，初始化
- 客户端模块 WDK 网络模块注册机构，注册
- 正在注册客户端模块
- 初始化客户端模块
- NmrRegisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01e7d2f1eb0ea343c27eef4d0d897bc2155d9037
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324944"
---
# <a name="initializing-and-registering-a-client-module"></a>初始化和注册客户端模块


它可以注册其自身与网络模块注册机构 (NMR) 之前，客户端模块必须初始化大量的数据结构。 这些结构包括[ **NPI\_MODULEID** ](https://msdn.microsoft.com/library/windows/hardware/ff568813)结构[ **NPI\_客户端\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff568812)结构[ **NPI\_注册\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff568815)结构 (包含在 NPI\_客户端\_特征结构)，并由客户端模块注册上下文使用的客户端模块定义的结构。

如果客户端模块向注册自身 NMR 的客户端作为[网络编程接口 (NPI)](network-programming-interface.md) ，用于定义特定于 NPI 的客户端特征，客户端模块还必须初始化客户端的实例特征 NPI 定义结构。

所有这些数据结构必须保持有效且驻留在内存中，只要向 NMR 注册客户端模块。

例如，假设"EXNPI"NPI 标头文件 Exnpi.h 中定义了以下：

```C++
// EXNPI NPI identifier
const NPIID EXNPI_NPIID = { ... };

// EXNPI client characteristics structure
typedef struct EXNPI_CLIENT_CHARACTERISTICS_
{
  .
  . // NPI-specific members
  .
} EXNPI_CLIENT_CHARACTERISTICS, *PEXNPI_CLIENT_CHARACTERISTICS;
```

下面显示了如何将自身注册为 EXNPI NPI 的客户端的客户端模块可以初始化所有这些数据结构：

```C++
// Include the NPI specific header file
#include "exnpi.h"

// Structure for the client module's NPI-specific characteristics
const EXNPI_CLIENT_CHARACTERISTICS NpiSpecificCharacteristics =
{
  .
  . // The NPI-specific characteristics of the client module
  .
};

// Structure for the client module's identification
const NPI_MODULEID ClientModuleId =
{
  sizeof(NPI_MODULEID),
  MIT_GUID,
  { ... }  // A GUID that uniquely identifies the client module
};

// Prototypes for the client module's callback functions
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

// Structure for the client module's characteristics
const NPI_CLIENT_CHARACTERISTICS ClientCharacteristics =
{
  0,
  sizeof(NPI_CLIENT_CHARACTERISTICS),
  ClientAttachProvider,
  ClientDetachProvider,
  ClientCleanupBindingContext,
  {
    0,
    sizeof(NPI_REGISTRATION_INSTANCE),
    &EXNPI_NPIID,
    &ClientModuleId,
    0,
    &NpiSpecificCharacteristics
  }
};

// Context structure for the client module's registration
typedef struct CLIENT_REGISTRATION_CONTEXT_ {
  .
  . // Client-specific members
  .
} CLIENT_REGISTRATION_CONTEXT, *PCLIENT_REGISTRATION_CONTEXT;

// Structure for the client's registration context
CLIENT_REGISTRATION_CONTEXT ClientRegistrationContext =
{
  .
  . // Initial values for the registration context
  .
};
```

客户端模块通常初始化单独存在于其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 客户端模块的主要初始化任务包括：

-   指定[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数。 当客户端模块是从系统中卸载时，操作系统将调用此函数。 如果客户端模块不提供卸载函数，不能从系统中卸载客户端模块。

-   调用[ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)函数向 NMR 注册客户端模块。

例如：

```C++
// Prototype for the client module's unload function
VOID
  Unload(
    PDRIVER_OBJECT DriverObject
    );

// Variable to contain the handle for the registration
HANDLE ClientHandle;

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

  // Register the client module with the NMR
  Status = NmrRegisterClient(
    &ClientCharacteristics,
    &ClientRegistrationContext,
    &ClientHandle
    );

  // Return the result of the registration
  return Status;
}
```

如果客户端模块的多个 NPI 客户端，它必须初始化一组独立的数据结构，并调用[ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)为它支持每个 NPI。 如果网络模块是客户端模块和提供程序模块 （也就是说，它是一个 NPI 的客户端和提供程序的另一个 NPI），它必须初始化两个独立的数据结构、 客户端界面和提供程序接口集并同时调用**NmrRegisterClient**并[ **NmrRegisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff568784)。

客户端模块不需要调用[ **NmrRegisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568782)中其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数。 例如，在其中客户端模块是一个复杂的驱动程序的子组件的情况下，客户端模块的注册时可能发生仅激活客户端模块子组件。

有关实现客户端模块的详细信息[ **Unload** ](https://msdn.microsoft.com/library/windows/hardware/ff564886)函数中，请参阅[卸载客户端模块](unloading-a-client-module.md)。

 

 





