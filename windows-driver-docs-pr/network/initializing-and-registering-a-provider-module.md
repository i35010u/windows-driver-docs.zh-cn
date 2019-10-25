---
title: 初始化和注册提供程序模块
description: 初始化和注册提供程序模块
ms.assetid: 967271ce-e4f5-45ce-9249-746d2fe698c1
keywords:
- 提供程序模块 WDK 网络模块注册程序，初始化
- 提供商模块 WDK 网络模块注册程序，注册
- 注册提供程序模块
- 初始化提供程序模块
- NmrRegisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02921de7125176883d16891d7c0295eeea1cf3ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824481"
---
# <a name="initializing-and-registering-a-provider-module"></a>初始化和注册提供程序模块


提供程序模块必须先初始化多个数据结构，然后才能将其自身注册到网络模块注册器（NMR）。 这些结构包括[**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))结构、 [**NPI\_提供程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_provider_characteristics)结构、 [**NPI\_注册\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)结构（包含在 NPI 中\_提供程序\_特征结构）以及由提供程序模块定义的、用于提供程序模块的注册上下文的结构。

如果提供程序模块将 NMR 作为[网络编程接口（NPI）](network-programming-interface.md)的提供程序注册，该接口定义了特定于 NPI 的提供程序特征，则提供程序模块还必须初始化提供程序特性的实例由 NPI 定义的结构。

只要提供程序模块已注册到 NMR，所有这些数据结构都必须保持有效并驻留在内存中。

例如，假设 "EXNPI" NPI 在头文件 Exnpi 中定义以下内容：

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

下面演示了如何将自身注册为 EXNPI NPI 的提供程序的提供程序模块可以初始化所有这些数据结构：

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

提供程序模块通常在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数内初始化自身。 提供程序模块的主要初始化任务是：

-   指定[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数。 从系统中卸载提供程序模块时，操作系统将调用此函数。 如果提供程序模块未提供 unload 函数，则无法从系统中卸载提供程序模块。

-   调用[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)函数，将提供程序模块注册到 NMR。

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

如果提供程序模块是多个 NPI 的提供程序，则它必须初始化一组独立的数据结构，并为它支持的每个 NPI 调用[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider) 。 如果网络模块既是提供商模块又是客户端模块（也就是说，它是一个 NPI 的提供程序，另一个 NPI 的客户端），则它必须初始化两个独立的数据结构集，一个用于提供程序接口，一个用于客户端接口，并同时调用**NmrRegisterProvider**和[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)。

提供程序模块不需要从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中调用[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider) 。 例如，在提供程序模块是复杂驱动程序的子组件的情况下，仅当激活提供程序模块子组件时，才会注册提供程序模块。

有关实现提供程序模块的[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数的详细信息，请参阅[卸载提供程序模块](unloading-a-provider-module.md)。

 

 





