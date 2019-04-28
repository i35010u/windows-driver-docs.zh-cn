---
title: 参与错误记录持久性
description: 参与错误记录持久性
ms.assetid: 06cbcccf-7cda-468d-aa6e-b8ecf95adf16
keywords:
- Windows 硬件错误体系结构 WDK，错误记录持久性
- WHEA WDK，错误记录持久性
- 硬件错误 WDK WHEA，错误记录持久性
- 错误 WDK WHEA，错误记录持久性
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误记录持久性
- PSHED 插件 WDK WHEA 错误记录持久性
- 错误记录持久性 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28a312a03f6b93a9f5abc4de84251ff612d0eca1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340774"
---
# <a name="participating-in-error-record-persistence"></a>参与错误记录持久性


若要参与错误记录持久性，PSHED 插件必须实现以下回调函数：

[*WriteErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff560678)

[*ReadErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff559476)

[*ClearErrorRecord*](https://msdn.microsoft.com/library/windows/hardware/ff559269)

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's WriteErrorRecord callback function
//
NTSTATUS
  WriteErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONG RecordLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if dummy write operation
  if (Flags & WHEA_WRITE_FLAG_DUMMY)
  {
    return STATUS_SUCCESS;
  }

  // Write the error record to the persistent data storage
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to write the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}

//
// The PSHED plug-in's ReadErrorRecord callback function
//
NTSTATUS
  ReadErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId,
    OUT ULONGLONG NextErrorRecordId,
    IN OUT PULONG RecordLength,
    IN OUT PWHEA_ERROR_RECORD ErrorRecord
    )
{
  ULONG Length;
  PWHEA_ERROR_RECORD Record;

  // Check if an error record that matches the
  // identifier in the ErrorRecordId parameter
  // exists in the persistent data storage
  if (...)
  {
    // Retrieve the length of the specified error
    // record from the persistent data storage
    Length = ...;

    // Check if the buffer is too small to contain
    // the error record
    if (*RecordLength < Length)
    {
      // Set the RecordLength to the required length
      *RecordLength = Length;

      // Return error status
      return STATUS_BUFFER_TOO_SMALL;
    }

    // Retrieve the error record from the
    // persistent data storage and copy it
    // into the buffer pointed to by the
    // ErrorRecord parameter.
    ...

    // If successful
    if (...)
    {
      // Set RecordLength to the length of the
      // error record
      *RecordLength = Length;

      // Check if there are any other error records
      // in the persistent data storage
      if (...)
      {
        // Return the identifier of the next
        // error record
        *NextErrorRecordId = ...;
      }

      // No other error records
      else
      {
        // Return the identifier of this error record
        *NextErrorRecordId = ErrorRecordId;
      }

      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to read the error record
    else
    {
      // Return error status
      return STATUS_UNSUCCESSFUL;
    }
  }

  // The error record does not exist in the
  // persistent data storage
  else
  {
    // Return error status
    return STATUS_OBJECT_NOT_FOUND;
  }
}

//
// The PSHED plug-in's ClearErrorRecord callback function
//
NTSTATUS
  ClearErrorRecord(
    IN OUT PVOID PluginContext,
    IN ULONG Flags,
    IN ULONGLONG ErrorRecordId
    )
{
  // Clear the error record that matches the specified
  // error record identifier from the persistent data
  // storage.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to clear the error record
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

必须指定插件参与错误记录持久性 PSHED **PshedFAErrorRecordPersistence**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

有关错误记录持久性的详细信息，请参阅[错误记录持久性机制](error-record-persistence-mechanism.md)。

 

 




