---
title: 初始化和注册客户端模块
description: 初始化和注册客户端模块
ms.assetid: 3d0941d0-5a6f-4c6d-b519-af850a8de341
keywords:
- 客户端模块 WDK 网络模块注册器，初始化
- 客户端模块 WDK 网络模块注册机构，注册
- 注册客户端模块
- 初始化客户端模块
- NmrRegisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d928d6e7b46c8364cc797a3040358dd65ed4cd40
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824484"
---
# <a name="initializing-and-registering-a-client-module"></a>初始化和注册客户端模块


客户端模块必须先初始化多个数据结构，然后才能将其自身注册到网络模块注册器（NMR）。 这些结构包括[**NPI\_MODULEID**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568813(v=vs.85))结构、 [**NPI\_客户端\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics)结构、 [**NPI\_注册\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance)结构（包含在 NPI 中\_客户端\_特征结构）以及由客户端模块定义的、用于客户端模块的注册上下文的结构。

如果客户端模块将 NMR 注册为定义 NPI 特定客户端特征的[网络编程接口（NPI）](network-programming-interface.md)的客户端，则客户端模块还必须初始化由定义的客户端特征结构的实例NPI。

只要向 NMR 注册了客户端模块，所有这些数据结构都必须保持有效并驻留在内存中。

例如，假设 "EXNPI" NPI 在头文件 Exnpi 中定义以下内容：

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

下面演示了将自身注册为 EXNPI NPI 的客户端的客户端模块可以初始化所有这些数据结构：

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

通常，客户端模块会在其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中进行初始化。 客户端模块的主要初始化任务如下：

-   指定[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数。 当从系统中卸载客户端模块时，操作系统将调用此函数。 如果客户端模块未提供 unload 函数，则无法从系统中卸载客户端模块。

-   调用[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient)函数以向 NMR 注册客户端模块。

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

如果客户端模块是多个 NPI 的客户端，则必须初始化一组独立的数据结构，并为它支持的每个 NPI 调用[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 。 如果网络模块同时是客户端模块和提供程序模块（即，它是一个 NPI 的客户端和另一个 NPI 的提供商），则它必须初始化两个独立的数据结构集，一个用于客户端接口，另一个用于提供程序接口，并同时调用**NmrRegisterClient**和[**NmrRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)。

不需要客户端模块从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中调用[**NmrRegisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 。 例如，在客户端模块是复杂驱动程序的子组件的情况下，客户端模块的注册仅在客户端模块子组件激活时才会发生。

有关实现客户端模块的[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)函数的详细信息，请参阅[卸载客户端模块](unloading-a-client-module.md)。

 

 





