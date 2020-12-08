---
title: 如何记录到全局记录器会话
description: 如何记录到全局记录器会话
keywords:
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 在启动过程中记录 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2241fed72b8aa7c25d453d4ecd989e1beda337b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809661"
---
# <a name="how-to-log-to-the-global-logger-session"></a>如何记录到全局记录器会话


使用以下过程将驱动程序配置为记录到全局记录器跟踪会话：

1. 将以下定义添加到驱动程序代码中。 在 [WPP \_ 控件 \_ guid](/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85)) 宏定义和 [跟踪消息头文件](trace-message-header-file.md)的 include 语句之间插入定义。
   ```
   #define WPP_GLOBALLOGGER
   ```

2. 使用 [Tracelog](tracelog.md) 配置全局记录器跟踪会话。 最简单的命令如下所示：

   ```
   tracelog -start GlobalLogger
   ```

   有关完整的说明，包括用于配置全局记录器跟踪会话的参数，请参阅 [**Tracelog 命令语法**](tracelog-command-syntax.md) 和 [全局记录器跟踪会话](global-logger-trace-session.md)。

   有关示例，请参阅 [示例13：创建全局记录器会话](example-13--creating-a-global-logger-session.md)。

   此命令创建并配置跟踪会话，但在重新启动系统 (步骤 5) 之前，会话不会启动。

3. 在 **HKLM \\ System \\ CurrentControlSet \\ control \\ WMI \\ GlobalLogger** 子项下，为跟踪提供程序的 [控件 GUID](control-guid.md) 添加一个名为的子项。 在 Windows Vista 和更高版本的 Windows 中，必须将控件 GUID 括在大括号中， ( {} ) 。

   **Tracelog GlobalLogger** 命令将 **GlobalLogger** 子项添加到注册表。 **ControlGUID** 子项将驱动程序建立为全局记录器跟踪会话的 [跟踪提供程序](trace-provider.md)。

   例如，若要将 Tracedrv 示例驱动程序配置为在运行 Windows XP 的计算机上记录到全局记录器跟踪会话，请添加一个名为 for Tracedrv control GUID、d58c126f-b309-11d1-969e-0000f875a5bc： **HKLM \\ SYSTEM \\ CurrentControlSet \\ control \\ WMI \\ GlobalLogger \\ d58c126f-b309-11d1-969e-0000f875a5bc** 的子项。

   [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，位于 GitHub 上的 [Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples) 存储库中。

4. 若要配置跟踪提供程序，请将以下注册表项添加到 **ControlGUID** 子项。 这些条目是可选的，它们的值由驱动程序定义。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">条目名称</th>
   <th align="left">数据类型</th>
   <th align="left">描述</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>标记</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定提供程序的 <a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a> 。</p>
   <p>标志的含义由每个跟踪提供程序单独定义。 通常，标志表示越来越详细的报表级别。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>级别</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定提供程序的 <a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a> 。</p>
   <p><strong>级别</strong>值的含义由每个跟踪提供程序单独定义。 通常，跟踪级别表示事件的严重性 (信息、警告或错误) 。</p></td>
   </tr>
   </tbody>
   </table>




请注意， **标志** 条目的名称是复数， **级别** 条目的名称是单数。


5.  重新启动系统。 这会启动全局记录器跟踪会话。

测试完成后，删除 **ControlGUID** 子项，或在 **GlobalLogger** 子项中将 **Start** 条目的值设置为0。 如果不这样做，则每次重新启动系统时，全局记录器会话都将运行，并且驱动程序将记录到其中。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

如果 \_ 存在 wpp GLOBALLOGGER，wpp 将添加读取注册表的代码，并确定全局记录器会话是否正在运行，以及是否启用了驱动程序以跟踪全局记录器会话。 此代码取代了驱动程序将从标准跟踪会话接收的启用通知。

此外，由于全局记录器会话不提供回调通知，因此 Windows 会假定回调已发生，并进行相应的处理。

WPP 定义只生成少量的代码，因此在测试后无需将其从代码中移除。
