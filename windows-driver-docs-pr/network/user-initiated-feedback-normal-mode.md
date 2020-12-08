---
title: 用户发起的反馈 - 正常模式
description: 本主题介绍在 WDI 驱动程序中通过 IHV 跟踪日志记录执行用户启动的反馈的正常模式。
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7628408048b0aac9e667efed65724c89351168db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783791"
---
# <a name="user-initiated-feedback---normal-mode"></a>用户发起的反馈 - 正常模式

在普通用户启动的反馈 (UIF) 情况下，用户遇到 Wi-Fi 的问题并提交反馈报告。 此报表收集 Wi-Fi 子系统的快照，包括 Wi-Fi WMI 自动记录器和网络统计信息等。为了收集特定于 IHV 的日志，Microsoft 提供了不带初始 ETW 提供程序的 WMI 自动记录器会话。 每个 IHV 都将其 ETW 提供程序集添加到 Microsoft 提供的 WMI 自动记录器会话注册表项下。 提交 UIF 报表后，将收集 IHV 自动记录器 ETL，并将其发送给 Microsoft 进行分析。 此日志文件是使用循环缓冲区实现的，该缓冲区的大小 (\< = 1mb) 。 应通过标志/级别/关键字适当地限制保存在此日志文件中的事件，以确保始终保存最近30分钟的日志事件。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供的 WMI 自动记录器会话

Microsoft 提供了不带初始 ETW 提供程序的 WMI 自动记录器会话。 安装 IHV 的驱动程序时，必须在 Microsoft 提供的 WMI 自动记录器会话密钥下添加所需的 WMI 提供程序注册表项。 IHV 不应更改任何自动记录器会话注册表值。 但是，所有 ETW 提供程序选项都可用于 IHV，包括 enable level、match any、match all 等。此日志记录会话始终运行并且具有有限的循环缓冲区，因此 Ihv 应正确设置提供程序 EnableLevels。

WMI 自动记录器会话已添加到具有以下路径的 HKLM 注册表配置单元：

`HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession`

生成的 ETL 日志文件位于以下位置：

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSession.etl`

## <a name="ihv-driver-inf-changes"></a>IHV 驱动程序 INF 更改

Ihv 需要更新其驱动程序 INF 文件来添加以下注册表项值，以便它们可以在 UIF 正常模式下获取详细的 IHV 日志。 以下代码片段提供了用于将单个 ETW 提供程序添加到自动记录器会话的模板。 IHV 可以添加尽可能多的提供程序。 此外，每个 ETW 提供程序的启用级别值都是特定于 IHV 的，因此它们不必与 Microsoft 定义的值相同 (TRACE_LEVEL_CRITICAL、TRACE_LEVEL_ERROR 等 ) 。

### <a name="enable-the-ihv-auto-logger-session"></a>启用 IHV 自动记录器会话

由于 IHV 自动记录器会话在没有 ETW 提供程序的情况下初始化，因此默认情况下禁用它。 需要使用 Ihv 来启用此会话，方法是将其驱动程序的 INF 文件中的 "Start" 值更新为 **1** ，如以下示例中所示：

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession,Start,%REG_DWORD%,1
```

### <a name="add-ihv-etw-providers"></a>添加 IHV ETW 提供程序

以下代码片段演示如何在 INF 文件中添加 IHV ETW 提供程序：

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,,EnableLevel,%REG_DWORD%,<IHV_LogEnableLevelValue>
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,MatchAnyKeyword,%REG_QWORD%,<IHV_MatchAnyKewordValue>

[The following is optional]
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\<IHVProviderGUID_1>,MatchAllKeyword,%REG_QWORD%,<IHV_MatchAllKewordValue>

[Strings]
REG_DWORD = 0x00010001
REG_QWORD = 0x000B0001
```

### <a name="example-values"></a>示例值

此示例阐释了本机 Wi-Fi 自定义级别设置 (启用所有) 所有本机 Wi-Fi 关键字：

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},,EnableLevel,%REG_DWORD%,0x04
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{0BD3506A-9030-4f76-9B88-3E8FE1F7CFB6},MatchAnyKeyword,%REG_QWORD%,0x000FFFFF

Standard EnableLevel values:
0x5 - Verbose
0x4 - Informational
0x3 - Warning
0x2 - Error
0x1 - Critical
0x0 – LogAlways
```

## <a name="related-links"></a>相关链接

[用户使用 IHV 跟踪日志记录发起的反馈](user-initiated-feedback-with-ihv-trace-logging.md)

[用户发起的反馈 - 再现模式](user-initiated-feedback-repro-mode.md)
