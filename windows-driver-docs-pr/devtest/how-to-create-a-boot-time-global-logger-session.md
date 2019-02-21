---
title: 如何创建启动时全局记录器会话
description: 如何创建启动时全局记录器会话
ms.assetid: ddd9e1b1-d732-4ef1-a0e0-4d8e95660d7c
keywords:
- 全局记录器跟踪会话 WDK，创建
- 启动时全局记录器跟踪会话 WDK，创建
- EnableKernelFlags WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3c4923f32b7f38f04c30f28ec8375168f42cbce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526391"
---
# <a name="how-to-create-a-boot-time-global-logger-session"></a>如何创建启动时全局记录器会话


若要创建记录内核事件的全局记录器跟踪会话的最简单方法是使用[Tracelog](tracelog.md)若要创建标准的全局记录器跟踪会话，然后再添加**EnableKernelFlags**条目并将其值。 本主题描述的过程。

1.  使用跟踪日志创建全局记录器跟踪会话。 最简单的命令如下所示：

    ```
    tracelog -start GlobalLogger
    ```

    有关说明和详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)并[全局记录器跟踪会话](global-logger-trace-session.md)。 有关示例，请参阅[示例 13:创建全局记录器会话](example-13--creating-a-global-logger-session.md)。

2.  添加 REG\_名为二进制条目**EnableKernelFlags**到**HKLM\\系统\\CurrentControlSet\\控件\\WMI\\GlobalLogger**子项。 创建 Tracelog **GlobalLogger**当你使用的注册表子项**tracelog-启动**命令。 可以使用的值**EnableKernelFlags**的值取自**EnableFlags**的成员**事件\_跟踪\_属性**结构。 有关的说明**EnableFlags**值，请参阅[**事件\_跟踪\_属性**](https://msdn.microsoft.com/library/windows/desktop/aa363784)。

3.  重新启动系统。

4.  测试完成后，使用**tracelog-删除**GlobalLogger 命令以重新初始化中的条目**GlobalLogger**子项。 否则，全局记录器跟踪会话每的次启动时启动系统。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

是否存在**EnableKernelFlags**条目，请使用有效的值，将转换为全局记录器跟踪会话 NT 内核记录器跟踪会话。 值**EnableKernelFlags**，以及其他全局记录器注册表项，用于将会话配置。 跟踪会话启动时重新启动系统。

注册表项用来配置全局记录器跟踪会话，因为系统是完全可操作之前，必须可配置值。

您可以通过编辑注册表或使用配置全局记录器跟踪会话[Tracelog](tracelog.md)，包含 Windows Driver Kit (WDK) 中的工具。 配置全局记录器跟踪会话的注册表项的详细信息，请参阅[全局记录器跟踪会话](global-logger-trace-session.md)。

运行后此跟踪会话，使用**tracelog-删除**命令设置的值**启动**为 0，以删除注册表子项添加条目。 如果不这样做，会话将运行每次启动系统，日志可能会变得很大。

有关跟踪日志命令的详细信息，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[**事件\_跟踪\_属性**](https://msdn.microsoft.com/library/windows/desktop/aa363784)

[示例 13:创建全局记录器会话](example-13--creating-a-global-logger-session.md)

[全局记录器跟踪会话](global-logger-trace-session.md)

[Tracelog](tracelog.md)

[**Tracelog 命令语法**](tracelog-command-syntax.md)

 

 






