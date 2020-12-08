---
title: 参与错误源发现
description: 参与错误源发现
keywords:
- Windows 硬件错误体系结构 WDK，错误源发现
- WHEA WDK，错误源发现
- 硬件错误 WDK WHEA，错误源发现
- 错误 WDK WHEA，错误源发现
- 平台特定硬件错误驱动程序插件 WDK WHEA，错误源发现
- PSHED 插件 WDK WHEA，错误源发现
- 错误源发现 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db4ebc8534e57a449dea5fb85c59fe083c8a3b1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787077"
---
# <a name="participating-in-error-source-discovery"></a>参与错误源发现


若要参与错误源发现，PSHED 插件必须实现 [*GetAllErrorSources*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_get_all_error_sources) 回调函数。 参与错误源发现的 PSHED 插件还可以实现可选的 [*GetErrorSourceInfo*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pshed_pi_get_error_source_info) 回调函数。

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's GetAllErrorSources callback function
//
NTSTATUS
  GetAllErrorSources(
    IN OUT PVOID PluginContext,
    IN OUT PULONG Count,
    IN OUT PWHEA_ERROR_SOURCE_DESCRIPTOR *ErrorSources,
    IN OUT PULONG Length
    )
{
  // Check if there is enough space remaining in the buffer
  // that contains the array of error source descriptors to 
  // include any additional error sources to be reported by
  // the PSHED plug-in.
  if (...)
  {
    // Update the list of error sources by modifying the
    // existing error sources in the list and adding any
    // additional error sources to the list.
    ...

    // If the number of error sources in the list has changed
    // update the count that is returned back to the kernel.
    *Count = ...;

    // If successful, return success status
    if (...)
    {
      return STATUS_SUCCESS;
    }

    // Failed to update the list of error sources
    else
    {
      return STATUS_UNSUCCESSFUL;
    }
  }

  // Insufficient space in the buffer.
  else
  {
    // Set the length the necessary buffer size
    *Length = ...;

    return STATUS_BUFFER_TOO_SMALL;
  }
}

//
// The PSHED plug-in's GetErrorSourceInfo callback function
//
NTSTATUS
  GetErrorSourceInfo(
    IN OUT PVOID PluginContext,
    IN OUT PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Modify the information contained in the
  // error source descriptor as appropriate.
  ...

  // If successful, return success status
  if (...)
  {
    return STATUS_SUCCESS;
  }

  // Failed to update the error source information
  else
  {
    return STATUS_UNSUCCESSFUL;
  }
}
```

参与错误源发现的 PSHED 插件在向操作系统 [注册](registering-a-pshed-plug-in.md)自身时必须指定 **PshedFADiscovery** 标志。

 

