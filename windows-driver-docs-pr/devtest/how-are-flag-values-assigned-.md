---
title: 如何分配的标志值
description: 如何分配的标志值
ms.assetid: de74e2d9-0ebf-4125-9dbb-42f7755010f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67eb4272f816cb41eb76980f9547e7d3e00b1a0f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358302"
---
# <a name="how-are-flag-values-assigned"></a>标志值是如何分配的？


[跟踪标志](trace-flags.md)由每个单独定义[跟踪提供程序](trace-provider.md)。 因此，一个提供程序的标志值可能意味着另一个提供程序完全不同的标志值的内容。 将值解释，您需要了解该提供程序。

通常情况下，跟踪标志表示越来越详细的报告级别。

标志值定义中 WPP\_定义\_位的元素[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏，例如如本例所示：

```
#define WPP_CONTROL_GUIDS \
    WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
        WPP_DEFINE_BIT(Error)  \
        WPP_DEFINE_BIT(Unusual)  \
        WPP_DEFINE_BIT(Noise) )
```

Windows 将分配给每个 WPP\_定义\_位元素以 1 开头的连续位值。 例如，它会将 1 分配给第二个位 （异常） 到 2 和 4 到第三位 （噪声） 的第一位 （错误）。

当您启动[跟踪会话](trace-session.md)，用于表示标志的位值。 例如，下面的命令使用[Tracelog](tracelog.md)若要启动跟踪会话[跟踪提供程序](trace-provider.md)之前定义。 它设置为 4 （噪声） 的标志值。

```
tracelog -start MyTrace -guid MyDriver.guid -flags 4
```









