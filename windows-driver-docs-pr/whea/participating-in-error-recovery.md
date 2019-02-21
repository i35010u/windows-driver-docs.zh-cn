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
ms.openlocfilehash: 0f5f4888fde97b7c1911ed5580828637c6a20919
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540789"
---
# <a name="participating-in-error-recovery"></a>参与错误恢复


若要参与错误恢复，PSHED 插件必须实现[ *AttemptRecovery* ](https://msdn.microsoft.com/library/windows/hardware/ff559257)回调函数。

下面的代码示例演示如何实现此回调函数。

```cpp
//
// The PSHED plug-in&#39;s AttemptRecovery callback function
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

 

 




