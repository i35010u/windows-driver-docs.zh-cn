---
title: 参与错误源控制
description: 参与错误源控制
ms.assetid: 4b2e3431-348f-48b1-924e-14b9fb5a48f0
keywords:
- Windows 硬件错误体系结构 WDK、 错误源控件
- WHEA WDK、 错误源控件
- 硬件错误 WDK WHEA，错误源代码管理
- 错误 WDK WHEA，错误源代码管理
- 特定于平台的硬件错误驱动程序插件 WDK WHEA，错误源代码管理
- PSHED 插件 WDK WHEA 错误源代码管理
- 错误源控制 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eb11e83460f6f4719bb93fba01d4b2e9a233d7a
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349286"
---
# <a name="participating-in-error-source-control"></a>参与错误源控制


若要参与错误源代码管理，PSHED 插件必须实现以下回调函数：

[*SetErrorSourceInfo*](https://msdn.microsoft.com/library/windows/hardware/ff559489)

[*EnableErrorSource*](https://msdn.microsoft.com/library/windows/hardware/ff559304)

[*DisableErrorSource*](https://msdn.microsoft.com/library/windows/hardware/ff559294)

下面的代码示例演示如何实现这些回调函数。

```cpp
//
// The PSHED plug-in's SetErrorSourceInfo callback function
//
NTSTATUS
  SetErrorSourceInfo(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports configuring
  // the specified error source.
  if (...)
  {
    // Save the new configuration data for the error
    // source in nonvolatile storage and apply the
    // configuration changes to the error source such
    // that they will become effective after the
    // system is restarted.
    ...

    // If successful, return success status
    if (...)
    {
      return STATUS_SUCCESS;
    }

    // Failed to configure the error source
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

//
// The PSHED plug-in's EnableErrorSource callback function
//
NTSTATUS
  EnableErrorSource(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports enabling
  // the specified error source.
  if (...)
  {
    // Enable the error source
    ...

    // If successful
    if (...)
    {
      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to enable the error source
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

//
// The PSHED plug-in's DisableErrorSource callback function
//
NTSTATUS
  DisableErrorSource(
    IN OUT PVOID PluginContext,
    IN PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSource
    )
{
  // Check if the plug-in supports disabling
  // the specified error source.
  if (...)
  {
    // Disable the error source
    ...

    // If successful
    if (...)
    {
      // Return success status
      return STATUS_SUCCESS;
    }

    // Failed to disable the error source
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

必须指定插件参与错误源控制 PSHED **PshedFAErrorSourceControl**标志时它[注册](registering-a-pshed-plug-in.md)与操作系统本身。

 

 




