---
title: 参与错误信息检索
description: 参与错误信息检索
ms.assetid: ed0ad20b-d978-4650-b3a0-6b0795323c77
keywords:
- Windows 硬件错误体系结构 WDK、 错误的信息检索
- WHEA WDK、 错误的信息检索
- 硬件错误 WDK WHEA，错误的信息检索
- 错误 WDK WHEA，错误的信息检索
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误的信息检索
- PSHED 插件 WDK WHEA 错误信息检索
- 错误的信息检索 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e57aef09a86ebcb0d20c934c99bcd066f7f49f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386462"
---
# <a name="participating-in-error-information-retrieval"></a>参与错误信息检索


若要参与错误信息检索，PSHED 插件必须实现以下回调函数：

[*RetrieveErrorInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_retrieve_error_info)

[*FinalizeErrorRecord*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_finalize_error_record)

[*ClearErrorStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_clear_error_status)

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

必须指定插件参与了错误的信息检索 PSHED **PshedFAErrorInfoRetrieval**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

 

 




