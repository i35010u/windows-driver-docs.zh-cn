---
title: 注册 PSHED 插件
description: 注册 PSHED 插件
ms.assetid: 8b710aa2-1477-4906-b5cb-d269d821ea28
keywords:
- 平台特定硬件错误驱动程序插件 WDK WHEA，注册
- 注册 PSHED 插件 WDK WHEA
- PSHED 插件 WDK WHEA，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3352727921342c6f03f1e2f792bea4246edac12d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207683"
---
# <a name="registering-a-pshed-plug-in"></a>注册 PSHED 插件


PSHED 插件通过调用 [**PshedRegisterPlugin**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pshedregisterplugin) 函数向 PSHED 注册自身，并传递指向已初始化 [**WHEA \_ PSHED \_ 插件 \_ 注册 \_ 包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pshed_plugin_registration_packet) 结构的指针。 PSHED 插件通常从其[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数或其[**AddDevice**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)函数内调用**PshedRegisterPlugin**函数。

在调用**PshedRegisterPlugin**之前，PSHED 插件可以调用[**PshedIsSystemWheaEnabled**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-pshedissystemwheaenabled)来检查系统是否已启用 WHEA。

PSHED 插件成功注册到 PSHED 后，无法在操作系统会话期间对其取消注册。 因此，不能从系统中卸载已注册的 PSHED 插件，否则可能会发生 bug 检查。 因此，PSHED 插件不实现 [**Unload**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 函数。

下面的代码示例演示如何注册参与错误信息检索和错误记录持久性的 PSHED 插件。

```cpp
// Prototypes for the callback functions for
// participating in error information retrieval
NTSTATUS
  RetrieveErrorInfo(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG64  BufferLength,
    IN OUT PWHEA_ERROR_PACKET  Packet
    );

NTSTATUS
  FinalizeErrorRecord(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG  BufferLength,
    IN OUT PWHEA_ERROR_RECORD  ErrorRecord
    );

NTSTATUS
  ClearErrorStatus(
    IN OUT PVOID  PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR  ErrorSource,
    IN ULONG  BufferLength,
    IN PWHEA_ERROR_RECORD  ErrorRecord
    );

// Prototypes for the callback functions for
// participating in error record persistence.
NTSTATUS
  WriteErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONG  RecordLength,
    IN PWHEA_ERROR_RECORD  ErrorRecord
    );

NTSTATUS
  ReadErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONGLONG  ErrorRecordId
    IN PULONGLONG  NextErrorRecordId
 IN OUT PULONG  RecordLength,
    OUT PWHEA_ERROR_RECORD  *ErrorRecord
    );

NTSTATUS
  ClearErrorRecord(
    IN OUT PVOID  PluginContext,
    IN ULONG  Flags,
    IN ULONGLONG  ErrorRecordId
    );

// The PSHED plug-in registration packet
WHEA_PSHED_PLUGIN_REGISTRATION_PACKET RegPacket =
{
  sizeof(WHEA_PSHED_PLUGIN_REGISTRATION_PACKET),
 WHEA_PLUGIN_REGISTRATION_PACKET_VERSION,
 NULL,
 PshedFAErrorInfoRetrieval | PshedFAErrorRecordPersistence,
  0,
  {
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    NULL,
    WriteErrorRecord,
    ReadErrorRecord,
    ClearErrorRecord,
    RetrieveErrorInfo,
    FinalizeErrorRecord,
    ClearErrorStatus,
    NULL,
    NULL,
    NULL
  }
}

//
// The PSHED plug-in's DriverEntry function
//
NTSTATUS
  DriverEntry(
    IN PDRIVER_OBJECT DriverObject,
    IN PUNICODE_STRING RegistryPath
    )
{
  BOOLEAN IsWheaEnabled;
  NTSTATUS Status;

  ...

  // No unload function
  DriverObject->DriverUnload = NULL;

  // Query if the system is WHEA-enabled
  IsWheaEnabled =
    PshedIsSystemWheaEnabled(
      );

  // Check result
  if (IsWheaEnabled == FALSE)
  {
    // Return "not supported" status
    return STATUS_NOT_SUPPORTED;
  }

  // Register the PSHED plug-in
  Status =
    PshedRegisterPlugin(
      &RegPacket
      );

  // Check status
  if (Status != STATUS_SUCCESS)
  {
    // Handle error
    ...
  }

  ...

  // Return success
  return STATUS_SUCCESS;
}
```

 

