---
title: 参与错误信息检索
description: 参与错误信息检索
ms.assetid: ed0ad20b-d978-4650-b3a0-6b0795323c77
keywords:
- Windows 硬件错误体系结构 WDK，错误信息检索
- WHEA WDK，错误信息检索
- 硬件错误 WDK WHEA，错误信息检索
- 错误 WDK WHEA，错误信息检索
- 平台特定硬件错误驱动程序插件 WDK WHEA、错误信息检索
- PSHED 插件 WDK WHEA，错误信息检索
- 错误信息检索 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5613cfa3f4d71d846c9688314fcd46eae0ee91c2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209473"
---
# <a name="participating-in-error-information-retrieval"></a>参与错误信息检索


若要参与检索错误信息，PSHED 插件必须实现以下回调函数：

[*RetrieveErrorInfo*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_retrieve_error_info)

[*FinalizeErrorRecord*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_finalize_error_record)

[*ClearErrorStatus*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_clear_error_status)

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's RetrieveErrorInfo callback function
//
NTSTATUS
  RetrieveErrorInfo(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource,
    IN ULONGLONG BufferLength,
    IN OUT PWHEA_ERROR_PACKET Packet
    )
{
  // Check if the plug-in supports retrieving error
  // information from the specified error source.
  if (...)
  {
    // Check if there is enough space remaining in the hardware
    // error packet to update it with the platform-specific
    // error information.
    if (...)
    {
      // Retrieve the platform-specific error information from
      // the error source and update the hardware error packet.
      ...

      // If successful, return success status
      if (...)
      {
        return STATUS_SUCCESS;
      }

      // Failed to retrieve the platform-specific error information
      else
      {
        return STATUS_UNSUCCESSFUL;
      }
    }

    // Insufficient space in the hardware error packet.
    else
    {
      return STATUS_BUFFER_TOO_SMALL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}

//
// The PSHED plug-in's FinalizeErrorRecord callback function
//
NTSTATUS
  FinalizeErrorRecord(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource,
    IN ULONG BufferLength,
    IN OUT PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if the plug-in supports finalizing the error
  // record for errors from the specified error source.
  if (...)
  {
    // Check if there is enough space remaining in the
    // error record to update it with the supplementary
    // platform-specific error record sections.
    if (...)
    {
      // Update the error record with the supplementary
      // platform-specific error record sections.
      ...

      // If successful, return success status
      if (...)
      {
        return STATUS_SUCCESS;
      }

      // Failed to update the error record
      else
      {
        return STATUS_UNSUCCESSFUL;
      }
    }

    // Insufficient space in the error record.
    else
    {
      return STATUS_BUFFER_TOO_SMALL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}

//
// The PSHED plug-in's ClearErrorStatus callback function
//
NTSTATUS
  ClearErrorStatus(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource,
    IN ULONG BufferLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if the plug-in supports clearing the error
  // status for errors from the specified error source.
  if (...)
  {
    // Clear the error status for the error source
    ...

    // If successful, return success status
    if (...)
    {
      return STATUS_SUCCESS;
    }

    // Failed to clear the error status
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Not supported by the plug-in
  else
  {
    return STATUS_NOT_SUPPORTED;
  }
}
```

参与错误信息检索的 PSHED 插件在向操作系统[注册](registering-a-pshed-plug-in.md)自身时必须指定**PshedFAErrorInfoRetrieval**标志。

 

