---
title: 如何创建启动时的全局记录器会话
description: 如何创建启动时的全局记录器会话
keywords:
- 全局记录器跟踪会话 WDK，创建
- 启动时全局记录器跟踪会话 WDK，创建
- EnableKernelFlags WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec78e510232e48dfff8d1447641c1116da8f27d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803581"
---
# <a name="how-to-create-a-boot-time-global-logger-session"></a>如何创建启动时的全局记录器会话


若要创建记录内核事件的全局记录器跟踪会话，最简单的方法是使用 [Tracelog](tracelog.md) 创建标准的全局记录器跟踪会话，然后添加 **EnableKernelFlags** 条目和其值。 本主题介绍了该过程。

1.  使用 Tracelog 创建全局记录器跟踪会话。 最简单的命令如下所示：

    ```
    tracelog -start GlobalLogger
    ```

    有关说明和详细信息，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md) 和 [全局记录器跟踪会话](global-logger-trace-session.md)。 有关示例，请参阅 [示例13：创建全局记录器会话](example-13--creating-a-global-logger-session.md)。

2.  向 \_ **HKLM \\ 系统 \\ CurrentControlSet \\ Control \\ WMI \\ GlobalLogger** 子项添加一个名为 **EnableKernelFlags** 的注册表项。 当你使用 **Tracelog** 命令时，Tracelog 会创建 **GlobalLogger** 注册表子项。 可用于 **EnableKernelFlags** 的值是从 **事件 \_ 跟踪 \_ 属性** 结构的 **EnableFlags** 成员的值中获取的。 有关 **EnableFlags** 值的说明，请参阅 [**事件 \_ 跟踪 \_ 属性**](/windows/desktop/ETW/event-trace-properties)。

3.  重新启动系统。

4.  测试完成后，使用 **tracelog-remove** GlobalLogger 命令重新初始化 **GlobalLogger** 子项中的项。 否则，每次启动系统时都会启动全局记录器跟踪会话。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

存在具有有效值的 **EnableKernelFlags** 项后，会将全局记录器跟踪会话转换为 NT 内核记录器跟踪会话。 **EnableKernelFlags** 的值以及其他全局记录器注册表项用于配置会话。 重新启动系统时，跟踪会话启动。

注册表项用于配置全局记录器跟踪会话，因为在系统完全操作之前配置值必须可用。

你可以通过编辑注册表或使用 [Tracelog](tracelog.md)（Windows 驱动程序工具包 (WDK) 中包含的工具来配置全局记录器跟踪会话。 有关配置全局记录器跟踪会话的注册表项的详细信息，请参阅 [全局记录器跟踪会话](global-logger-trace-session.md)。

运行此跟踪会话后，使用 **tracelog** 命令将 **开始** 项的值设置为0，以删除添加的注册表子项。 如果没有这样做，则每次启动系统时都会运行该会话，并且日志可能会增长得非常大。

有关 Tracelog 命令的详细信息，请参阅 [ **Tracelog 命令语法**](tracelog-command-syntax.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**事件 \_ 跟踪 \_ 属性**](/windows/desktop/ETW/event-trace-properties)

[示例 13：创建全局记录器会话](example-13--creating-a-global-logger-session.md)

[全局记录器跟踪会话](global-logger-trace-session.md)

[Tracelog](tracelog.md)

[**Tracelog 命令语法**](tracelog-command-syntax.md)

 

