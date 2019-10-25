---
title: 参与错误恢复
description: 参与错误恢复
ms.assetid: 79f534b2-a5eb-4249-bfff-2f40c25805a6
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
ms.openlocfilehash: 9037cf42b8190ff4436fc1627a088b481a24933f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826184"
---
# <a name="participating-in-error-recovery"></a>参与错误恢复


若要参与错误恢复，PSHED 插件必须实现[*AttemptRecovery*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_attempt_error_recovery)回调函数。

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

参与错误恢复的 PSHED 插件在向操作系统[注册](registering-a-pshed-plug-in.md)自身时必须指定**PshedFAErrorRecovery**标志。

 

 




