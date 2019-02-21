---
title: 用户启动的反馈-正常模式
description: 本主题介绍 IHV 跟踪 WDI 驱动程序中的日志记录与标准用户启动反馈的模式。
ms.assetid: 723732A3-4B24-4FE5-B338-B8443F287FDE
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d27dd6793cc76611243ba7a6745e3f05d49be3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525819"
---
# <a name="user-initiated-feedback---normal-mode"></a>用户启动的反馈-正常模式

在正常用户启动反馈 (UIF) 方案中，用户体验问题的 Wi-fi 和提交反馈报表。 此报表收集的 Wi-fi 子系统，包括 Wi-fi WMI 自动记录器、 网络统计信息等的快照。若要收集 IHV 特定的日志，Microsoft 提供了与没有初始的 ETW 提供程序的 WMI 自动记录器会话。 每个 IHV 将他们的 ETW 提供程序由 Microsoft 提供的 WMI 自动记录器会话注册表项之下。 当提交 UIF 报表时，IHV 自动-记录器 ETL 收集并发送给 Microsoft 进行分析。 此日志文件实现使用一个循环缓冲区，以及相当有限大小 (\<= 1 MB)。 在此日志文件中保存的事件应适当地通过标志/级别/关键字来确保至少 30 分钟的日志事件始终保存在过去受到限制。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供 WMI 自动记录器会话

Microsoft 提供了与没有初始的 ETW 提供程序的 WMI 自动记录器会话。 IHV 的驱动程序安装时，它们必须添加的所需的 WMI 提供程序注册表项下由 Microsoft 提供的 WMI 自动记录器会话密钥。 IHV 不应更改任何自动记录器会话注册表值。 但是，所有 ETW 提供程序选项都可供包括启用级别 IHV、 与任何匹配、 匹配所有，等等。此日志记录会话应始终运行，并具有有限的循环缓冲区，因此 Ihv 应适当地设置 EnableLevels 的提供程序。

WMI 自动记录器会话添加到具有以下路径的 HKLM 注册表配置单元：

`HKLM\SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession`

生成的 ETL 日志文件的位置如下：

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSession.etl`

## <a name="ihv-driver-inf-changes"></a>IHV 驱动程序 INF 更改

Ihv 需要更新其驱动程序 INF 文件，添加以下注册表项值，以便他们可以在 UIF 正常模式期间获取详细 IHV 日志。 以下代码片段将单个 ETW 提供程序添加到自动记录器会话提供的模板。 IHV 可以添加任意多个提供商，他们认为适合。 此外，启用级别值 IHV 特定于每个 ETW 提供程序，因此，他们就不需要一定会 （TRACE_LEVEL_CRITICAL、 TRACE_LEVEL_ERROR 等） 的 Microsoft 定义的值相同。

### <a name="enable-the-ihv-auto-logger-session"></a>启用 IHV 自动记录器会话

与任何 ETW 提供程序初始化 IHV 自动记录器会话，因为默认情况下禁用。 通过更新到"开始"值来启用此会话所需的 Ihv **1**在其驱动程序的 INF 文件中，在此示例中所示：

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

此示例说明了与所有本机 Wi-fi 关键字的本机 Wi-fi 自定义级设置 （启用所有）：

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

[用户启动使用 IHV 跟踪日志记录的反馈](user-initiated-feedback-with-ihv-trace-logging.md)

[用户启动的反馈-重现模式](user-initiated-feedback-repro-mode.md)
