---
title: 如何登录到全局记录器会话
description: 如何登录到全局记录器会话
ms.assetid: b5efea00-39cd-4df3-aac4-ade9126f69ed
keywords:
- 全局记录器跟踪会话 WDK，日志记录
- 启动时全局记录器跟踪会话 WDK，日志记录
- 启动过程中日志 WDK 跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3586e9ac23a2c38be1067a0a8520b2ac91b88bfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540555"
---
# <a name="how-to-log-to-the-global-logger-session"></a>如何登录到全局记录器会话


使用以下过程配置的驱动程序将记录到全局记录器跟踪会话：

1. 将以下定义添加到驱动程序代码。 插入之间定义[WPP\_控制\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)宏定义和 include 语句[跟踪消息标头文件](trace-message-header-file.md)。
   ```
   #define WPP_GLOBALLOGGER
   ```

2. 使用[Tracelog](tracelog.md)配置全局记录器跟踪会话。 最简单的命令如下所示：

   ```
   tracelog -start GlobalLogger
   ```

   有关完整说明，包括用于配置全局记录器跟踪会话，参数，请参阅[ **Tracelog 命令语法**](tracelog-command-syntax.md)并[全局记录器跟踪会话](global-logger-trace-session.md)。

   有关示例，请参阅[示例 13:创建全局记录器会话](example-13--creating-a-global-logger-session.md)。

   此命令创建并配置跟踪会话，但会话不会启动，直到重新启动系统 （步骤 5）。

3. 下**HKLM\\系统\\CurrentControlSet\\控制\\WMI\\GlobalLogger**子项中，添加名为的一个子项[控制 GUID](control-guid.md)跟踪提供程序。 在 Windows Vista 和更高版本的 Windows 中，控件 GUID 必须括在大括号 ( {} )。

   **Tracelog-启动 GlobalLogger**命令将添加**GlobalLogger**对注册表子项。 **ControlGUID**子项建立驱动程序，因为[跟踪提供程序](trace-provider.md)全局记录器跟踪会话。

   例如，若要配置 Tracedrv 示例驱动程序，能够登录到运行 Windows XP 的计算机上的全局记录器跟踪会话，请添加名为 Tracedrv 控件 GUID，d58c126f-b309-11 d 1 969e 0000f875a5bc 的一个子项：**HKLM\\系统\\CurrentControlSet\\控件\\WMI\\GlobalLogger\\d58c126f-b309-11d1-969e-0000f875a5bc**。

   [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub 上的存储库。

4. 若要配置跟踪提供程序，添加到以下注册表项**ControlGUID**子项。 这些条目是可选的它们的值定义由驱动程序。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">项名称</th>
   <th align="left">数据类型</th>
   <th align="left">描述</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>标志</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">跟踪标志</a>提供程序。</p>
   <p>标志的含义是单独定义的每个跟踪提供程序。 通常情况下，标志表示越来越详细的报告级别。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Level</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">跟踪级别</a>提供程序。</p>
   <p>含义<strong>级别</strong>值单独定义每个跟踪提供程序。 通常情况下，跟踪级别表示 （信息、 警告或错误） 事件的严重性。</p></td>
   </tr>
   </tbody>
   </table>




请注意的名称**标志**条目，并且复数形式的名称**级别**条目为单数形式。


5.  重新启动系统。 这将启动全局记录器跟踪会话。

测试完成后，删除**ControlGUID**子项或的值设置**启动**中的条目**GlobalLogger**子项为 0。 如果不这样做，则全局记录器将会话运行，并且驱动程序日志，每次重新启动系统。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

当 WPP\_GLOBALLOGGER 存在，WPP 添加代码，读取注册表，并确定是否全局记录器会话正在运行以及是否为全局记录器会话跟踪启用驱动程序。 此代码进行驱动程序会收到从标准跟踪会话启用通知。

此外，由于全局记录器会话不会提供回调通知，Windows 假定回调发生，并相应地继续。

WPP 定义生成仅少量的代码，因此无需测试完成后删除它们的代码。









