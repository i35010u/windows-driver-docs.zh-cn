---
title: 初始化和注册客户端模块
description: 初始化和注册客户端模块
keywords:
- 客户端模块 WDK 网络模块注册器，初始化
- 客户端模块 WDK 网络模块注册机构，注册
- 注册客户端模块
- 初始化客户端模块
- NmrRegisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c4d8960deef9b22776a32318fe268d9aea47263
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803685"
---
# <a name="initializing-and-registering-a-client-module"></a>初始化和注册客户端模块


客户端模块必须先初始化多个数据结构，然后才能将其自身注册到网络模块注册器 (NMR) 。 这些结构包括 [**NPI \_ MODULEID**](/previous-versions/windows/hardware/drivers/ff568813(v=vs.85)) 结构、 [**NPI \_ 客户端 \_ 特征**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_client_characteristics) 结构、 [**NPI \_ 注册 \_ 实例**](/windows-hardware/drivers/ddi/netioddk/ns-netioddk-_npi_registration_instance) 结构 (包含在 NPI \_ 客户端 \_ 特征结构) 中，以及由客户端模块定义的、用于客户端模块的注册上下文的结构。

如果客户端模块将 NMR 作为网络编程接口的客户端注册 [ (NPI) ](network-programming-interface.md) 来定义 NPI 特定的客户端特征，则客户端模块还必须初始化 NPI 定义的客户端特征结构的实例。

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

通常，客户端模块会在其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数中进行初始化。 客户端模块的主要初始化任务如下：

-   指定 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数。 当从系统中卸载客户端模块时，操作系统将调用此函数。 如果客户端模块未提供 unload 函数，则无法从系统中卸载客户端模块。

-   调用 [**NmrRegisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 函数以向 NMR 注册客户端模块。

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

如果客户端模块是多个 NPI 的客户端，则必须初始化一组独立的数据结构，并为它支持的每个 NPI 调用 [**NmrRegisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 。 如果网络模块同时是客户端模块和提供程序模块 (也就是说，它是一个 NPI 的客户端，另一个 NPI) 的提供程序，则它必须初始化两个独立的数据结构集，一个用于客户端接口，一个用于提供程序接口，并同时调用 **NmrRegisterClient** 和 [**NmrRegisterProvider**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterprovider)。

不需要客户端模块从其 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数中调用 [**NmrRegisterClient**](/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrregisterclient) 。 例如，在客户端模块是复杂驱动程序的子组件的情况下，客户端模块的注册仅在客户端模块子组件激活时才会发生。

有关实现客户端模块的 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数的详细信息，请参阅 [卸载客户端模块](unloading-a-client-module.md)。

 

