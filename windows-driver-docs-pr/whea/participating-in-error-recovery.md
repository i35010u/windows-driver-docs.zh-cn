---
title: 参与错误恢复
description: 参与错误恢复
keywords:
- Windows 硬件错误体系结构 WDK，错误恢复
- WHEA WDK，错误恢复
- 硬件错误 WDK WHEA，错误恢复
- 错误 WDK WHEA，错误恢复
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误恢复
- PSHED 插件 WDK WHEA，错误恢复
- 错误恢复 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fdb60777fd30e0f370172744420f032890fc9c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787091"
---
# <a name="participating-in-error-recovery"></a>参与错误恢复


若要参与错误恢复，PSHED 插件必须实现 [*AttemptRecovery*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_attempt_error_recovery) 回调函数。

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

参与错误恢复的 PSHED 插件在向操作系统 [注册](registering-a-pshed-plug-in.md)自身时必须指定 **PshedFAErrorRecovery** 标志。

 

