---
title: 如何分配标志值
description: 如何分配标志值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307a0b5275a1a9df58c8fcd0a97997ae34c8289c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831559"
---
# <a name="how-are-flag-values-assigned"></a>标志值是如何分配的？


[跟踪标志](trace-flags.md) 由每个 [跟踪提供程序](trace-provider.md)单独定义。 因此，一个提供程序的标志值可能与另一个提供程序的标志值完全不同。 若要解释这些值，你需要了解该访问接口。

通常，跟踪标志表示越来越详细的报表级别。

标记值是在 wpp \_ 定义 \_ [wpp \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏的位元素中定义的，如本示例中所示：

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(Error)  \
        WPP_DEFINE_BIT(Unusual)  \
        WPP_DEFINE_BIT(Noise) )
```

Windows 向每个 WPP \_ 分配 \_ 一个以1开头的连续位值。 例如，它会将第一位赋给第一位 (错误) ，2到第二位 (异常) ，4到第三位 (干扰。

启动 [跟踪会话](trace-session.md)时，请使用位值表示标志。 例如，下面的命令使用 [Tracelog](tracelog.md) 通过前面定义的 [跟踪提供程序](trace-provider.md) 来启动跟踪会话。 它将标志值设置为 4 (噪音) 。

```
tracelog -start MyTrace -guid MyDriver.guid -flags 4
```
