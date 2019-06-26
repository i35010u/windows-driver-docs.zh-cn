---
title: 参与错误恢复
description: 参与错误恢复
ms.assetid: 79f534b2-a5eb-4249-bfff-2f40c25805a6
keywords:
- Windows 硬件错误体系结构 WDK，错误恢复
- WHEA WDK，错误恢复
- 硬件错误 WDK WHEA，错误恢复
- 错误 WDK WHEA，错误恢复
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误恢复
- PSHED 插件 WDK WHEA 错误恢复
- 错误恢复 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: def79e808f5256e4e2d2a10dd91dd5b44ef94c25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386454"
---
# <a name="participating-in-error-recovery"></a>参与错误恢复


若要参与错误恢复，PSHED 插件必须实现[ *AttemptRecovery* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_attempt_error_recovery)回调函数。

下面的代码示例演示如何实现此回调函数。

```cpp
//
// The PSHED plug-in's AttemptRecovery callback function
//
NTSTATUS
  AttemptRecovery(
    IN OUT PVOID PluginContext,
    IN ULONG BufferLength,
    IN PWHEA_ERROR_RECORD ErrorRecord
    )
{
  // Check if the error condition was not corrected by the
  // operating system or by the PSHED.
  if (ErrorRecord->Header.Severity != WheaErrSevCorrected)
  {
    // Attempt to correct the error condition.
    ...

    // If not successful, return failure status
    if (...)
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Perform any additional operations that are required
  // to fully recover from the error condition.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to fully recover from the error condition
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

必须指定插件参与错误恢复 PSHED **PshedFAErrorRecovery**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

 

 




