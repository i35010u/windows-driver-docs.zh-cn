---
title: 参与错误源发现
description: 参与错误源发现
ms.assetid: 349c8f06-be79-4a40-8b9f-cbefc563f6de
keywords:
- Windows 硬件错误体系结构 WDK、 错误源发现
- WHEA WDK、 错误源发现
- 硬件错误 WDK WHEA，错误源发现
- WDK WHEA，错误源发现的错误
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误源发现
- PSHED 插件 WDK WHEA 错误源发现
- 错误源发现 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55743724efa39befa3e190ff105f74ddb7915dee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340765"
---
# <a name="participating-in-error-source-discovery"></a>参与错误源发现


若要参与错误源发现，PSHED 插件必须实现[ *GetAllErrorSources* ](https://msdn.microsoft.com/library/windows/hardware/ff559366)回调函数。 参与错误源发现 PSHED 插件还可以实现的可选[ *GetErrorSourceInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559368)回调函数。

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

必须指定插件参与错误源发现 PSHED **PshedFADiscovery**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

 

 




