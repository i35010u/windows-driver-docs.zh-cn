---
title: 参与错误注入
description: 参与错误注入
ms.assetid: 0bd9efbd-e98d-457a-a28f-e09dcb5ae24d
keywords:
- Windows 硬件错误体系结构 WDK，错误注入
- WHEA WDK，错误注入
- 硬件错误 WDK WHEA，错误注入
- 错误 WDK WHEA，错误注入
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误注入
- PSHED 插件 WDK WHEA 错误注入
- 错误注入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1163a64508a4f003f3ad12d76d81925cff0c762d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386456"
---
# <a name="participating-in-error-injection"></a>参与错误注入


若要参与错误信息检索，PSHED 插件必须实现以下回调函数：

[*GetInjectionCapabilities*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_get_injection_capabilities)

[*InjectError*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-pshed_pi_inject_error)

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's GetInjectionCapabilities callback function
//
NTSTATUS
  GetInjectionCapabilities(
    IN OUT PVOID PluginContext,
    OUT PWHEA_ERROR_INJECTION_CAPABILITIES Capabilities
    )
{
  // Set the members in the structure pointed to by the
  // Capabilities parameter to indicate the error injection
  // capabilities supported by the PSHED plug-in.
  ...

  // Return success status
  return STATUS_SUCCESS;
}

//
// The PSHED plug-in's InjectError callback function
//
NTSTATUS
  InjectError(
    IN OUT PVOID PluginContext,
    IN ULONG ErrorType,
 IN ULONGLONG Parameter1,
    IN ULONGLONG Parameter2,
    IN ULONGLONG Parameter3,
    IN ULONGLONG Parameter4
    )
{
  // Inject the hardware error specified in the ErrorType
  // parameter into the hardware platform.
  // Parameter1 through Parameter4 contain any additional
  // data that is required to inject the error.
  ...

  // Note: For injected errors that are fatal or otherwise
  // unrecoverable, this callback function might not continue
  // execution past this point before the Windows kernel
  // generates a bug check in response to the error condition.

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
```

必须指定插件参与错误注入 PSHED **PshedFAErrorInjection**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

 

 




