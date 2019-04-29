---
title: 用户发起的反馈 - 再现模式
description: 本主题介绍 IHV 跟踪 WDI 驱动程序中的日志记录用户启动反馈重现的模式。
ms.assetid: C9784C2D-75B1-4229-A219-748C52F430D5
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 48331866a493beda962b0d9334ec5c57c544697f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362503"
---
# <a name="user-initiated-feedback---repro-mode"></a>用户发起的反馈 - 再现模式

用户启动反馈 (UIF) 重现模式允许系统以收集更详细日志记录时用户重现 bug。 如 UIF 正常模式下，这也可以通过使用 IHV 定义 ETW 提供程序创建新的 WMI 日志记录会话。 重现模式完成后，详细日志收集并发送给 Microsoft 进行分析。 没有用于启用或禁用详细固件日志 IHV 扩展点。 重现日志用于更多详细信息，以便能够跟踪客户有问题的原因。 因此，重现模式日志的日志文件大小设置为最大大小为 10 MB。 IHV 应使用 ETW 提供程序标志/级别/关键字值的更详细的设置。

当前 UIF 重现模式模型要求之前 IHV 反馈日志将包括 Microsoft 的所有提供程序 Guid、 级别和标记通知。 将提供程序添加到注册表，如本主题中所示启用 IHV 若要测试的适当级别的日志。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供 WMI 自动记录器会话

Microsoft 提供了与没有初始的 ETW 提供程序的 WMI 自动记录器会话。 IHV 的驱动程序安装时，它们必须添加的所需的 WMI 提供程序注册表项下由 Microsoft 提供的 WMI 自动记录器会话密钥。 IHV 不应更改任何自动记录器会话注册表值。 但是，所有 ETW 提供程序选项都可供包括启用级别 IHV、 与任何匹配、 匹配所有，等等。

> [!IMPORTANT]
> 作为自动记录器永远不会启用自动记录器。 使用这些值来验证重现模式 IHV 日志记录中所述[测试重现模式日志](#testing-the-repro-mode-logs)。 此外，我们可能会要求用户通过使用手动提交这些日志`netsh`工具。 提供程序 Guid、 级别和标志必须还在提交给 Microsoft，以及一个示例日志，因此它们会包括在重现模式 UIFs (请参阅[向 Microsoft 提交 IHV 提供程序](#submitting-ihv-providers-to-microsoft)。

WMI 自动记录器会话添加到具有以下路径的 HKLM 注册表配置单元：

`HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSessionRepro`

生成的 ETL 日志文件的位置如下：

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSessionRepro.etl`

## <a name="ihv-driver-inf-changes"></a>IHV 驱动程序 INF 更改

Ihv 需要更新其驱动程序 INF 文件，添加以下注册表项值，以便他们可以在 UIF 正常模式期间获取详细 IHV 日志。 以下代码片段将单个 ETW 提供程序添加到自动记录器会话提供的模板。 IHV 可以添加任意多个提供商，他们认为适合。 此外，启用级别值 IHV 特定于每个 ETW 提供程序，因此，他们就不需要一定会 （TRACE_LEVEL_CRITICAL、 TRACE_LEVEL_ERROR 等） 的 Microsoft 定义的值相同。

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

此示例演示使用的所有关键字 WDI UE 条信息性级别设置：

```INF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},Enabled,%REG_DWORD%,1
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},,EnableLevel,%REG_DWORD%,0xFF
HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSession\{21ba7b61-05f8-41f1-9048-c09493dcfe38},MatchAnyKeyword,%REG_QWORD%,0x000FFFFF

Standard EnableLevel values:
0x5 - Verbose
0x4 - Informational
0x3 - Warning
0x2 - Error
0x1 - Critical
0x0 – LogAlways
```

## <a name="etw-control-callback"></a>ETW 控制回调

IHV 可以注册其 ETW 日志记录代码中的 ETW 控制回调。 这使得 IHV ETW 提供程序启用、 禁用，或启动捕获控件时收到通知。 这样一来，IHV 可以打开或关闭重现模式的详细固件日志。

> [!NOTE]
> 如果正常和重现模式之间共享的 ETW 提供程序，应关闭 IHV 定义 EnableLevel，定义在 INF 文件中，若要启动/停止详细固件日志密钥 IHV。

### <a name="etw-callback-function"></a>ETW 的回调函数

以下代码片段演示如何注册回调的 ETW。 这是仅重要如果 IHV 需要执行特殊操作期间的开始和结束 UIF 重现模式 （如启动或停止日志记录详细固件）。 如果使用多个 ETW 提供程序，Ihv 可以考虑仅实现一个回调以启动固件日志记录。 将所有固件记录必须都路由到 IHV 的 ETW 跟踪提供程序。 UIF 的诊断工具将仅收集 IHV 的 ETW 提供程序跟踪。

有两种方法来启用 ETW 回调，具体取决于如何实现 ETW 日志记录。

1. 使用自动生成的代码通过表现 ETWs `MC.exe`。 请参阅[编写检测清单](https://msdn.microsoft.com/library/windows/desktop/dd996930)的更多详细信息。
    1. 以下代码片段 (etwtracingevents.h) 中的标头是已通过创建一个自动生成 ETW 事件标头`MC.exe`。 假定，已经生成的 ETW 事件，因此本主题不会重点此部分。
    1. 必须包括自动生成 ETW 标头之前定义 MCGEN_PRIVATE_ENABLE_CALLBACK_V2。 否则，不会调用回调。
1. 通过 ETW 回调注册[ **EventRegister** ](https://msdn.microsoft.com/library/windows/desktop/aa363744) API。
    1. ETW 回调提供程序必须将传递给**EventRegister**时注册跟踪提供程序的功能。

此代码段显示了 ETW 回调函数的原型。

```C++
#include <evntprov.h>
extern
VOID
EtwEventControlCallback(
    _In_ LPCGUID SourceId,
    _In_ ULONG ControlCode,
    _In_ UCHAR Level,
    _In_ ULONGLONG MatchAnyKeyword,
    _In_ ULONGLONG MatchAllKeyword,
    _In_opt_ PEVENT_FILTER_DESCRIPTOR FilterData,
    _Inout_opt_ PVOID CallbackContext
    );
```

下面的代码只是如果您使用，则使用自动生成的 ETW 事件需要`MC.exe`工具。

```C++
#define MCGEN_PRIVATE_ENABLE_CALLBACK_V2 EtwEventControlCallback

#include "etwtracingEvents.h" // Generated from manifest - This must come 
                              // after MCGEN_PRIVATE_ENABLE_CALLBACK_V2 is                   
                              // defined
```

*ControlCode* ETW 回调的参数指示当启用或禁用该提供程序。 在中定义的值`<evntrace.h>`且具有以下值：

```C++
#define EVENT_CONTROL_CODE_DISABLE_PROVIDER 0
#define EVENT_CONTROL_CODE_ENABLE_PROVIDER  1
#define EVENT_CONTROL_CODE_CAPTURE_STATE    2
```

#### <a name="eventcontrolcodeenableprovider"></a>EVENT_CONTROL_CODE_ENABLE_PROVIDER

此标志启用 ETW 提供程序，并指示 UIF 重现模式会话已启动。 这应该用于启动固件详细日志记录和/或数据包日志记录。

#### <a name="eventcontrolcodedisableprovider"></a>EVENT_CONTROL_CODE_DISABLE_PROVIDER

此标志禁用 ETW 提供程序，并指示 UIF 重现模式会话已结束。 IHV 的实现应刷新和如果此时重置固件日志*级别*参数匹配的 INF 文件 (在下一节的示例中为 0xFF) 中的 IHV 指定 UIF 重现模式级别。

#### <a name="eventcontrolcodecapturestate"></a>EVENT_CONTROL_CODE_CAPTURE_STATE

此标志请求提供程序记录其状态信息。 这通常称为将内存中日志刷新到磁盘。 IHV 的实现应刷新和如果此时重置固件日志*级别*参数匹配的 INF 文件 (在下一节的示例中为 0xFF) 中的 IHV 指定 UIF 重现模式级别。

### <a name="sample-code"></a>示例代码

以下是可用作模板来启用详细的驱动程序和固件的 UIF 重现模式方案的日志记录的示例 ETW 回调实现。

> [!NOTE]
> Ihv 需要刷新所有挂起的固件日志都**EVENT_CONTROL_CODE_CAPTURE_STATE**并**EVENT_CONTROL_CODE_DISABLE_PROVIDER**控制代码。

之后**EVENT_CONTROL_CODE_CAPTURE_STATE**是调用，UIF 诊断工具调用 ETW 回调两个更多时间与**EVENT_CONTROL_CODE_ENABLE_PROVIDER**控制代码。 因此，若要避免重新启用固件日志记录，状态机将从移动*ReproModeStateCaptured*状态变为*ReproModeStateFinal*状态之前将移回*ReproModeStateNotStarted*状态。 **EVENT_CONTROL_CODE_DISABLE_PROVIDER**控制代码仅用于禁用此提供程序。 这不是 UIF 过程的一部分，但仍需要将接受。

应更改 Ihv **IHV_ETW_REPRO_MODE_LEVEL**值在下面的示例以匹配在 INF 文件中设置的重现模式级别。

```C++
#define IHV_ETW_REPRO_MODE_LEVEL 0xFF // This value must match the repro mode              
                                      // EnableLevel INF value

typedef enum _EtwReproModeState
{
    ReproModeStateNotStarted = 0,
    ReproModeStateStarted,
    ReproModeStateCaptured,
    ReproModeStateFinal
} EtwReproModeState;
 
static EtwReproModeState g_eReproModeLoggingEnabled = ReproModeStateNotStarted; 

VOID
EtwEventControlCallback(
    _In_ LPCGUID SourceId,
    _In_ ULONG ControlCode,
    _In_ UCHAR Level,
    _In_ ULONGLONG MatchAnyKeyword,
    _In_ ULONGLONG MatchAllKeyword,
    _In_opt_ PEVENT_FILTER_DESCRIPTOR FilterData,
    _Inout_opt_ PVOID CallbackContext
    )
{
    UNREFERENCED_PARAMETER(SourceId);
    UNREFERENCED_PARAMETER(MatchAnyKeyword);
    UNREFERENCED_PARAMETER(MatchAllKeyword);
    UNREFERENCED_PARAMETER(FilterData);
    UNREFERENCED_PARAMETER(CallbackContext);

    switch(ControlCode)
    {
        case EVENT_CONTROL_CODE_ENABLE_PROVIDER:
            if (Level == IHV_ETW_REPRO_MODE_LEVEL)
            {
                switch(g_eReproModeLoggingEnabled)
                {
                    case ReproModeStateNotStarted:
                        //
                        // Enable verbose Firmware logs.
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateStarted;
                        break;

                    case ReproModeStateCaptured:
                        //
                        // The diagnostic tools will invoke the callback after
                        // the capture with EVENT_CONTROL_CODE_ENABLE_PROVIDER
                        // twice. 
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateFinal;
                        break;

                    case ReproModeStateFinal:
                        //
                        // The state machine is now complete, reset the state.
                        //
                        g_eReproModeLoggingEnabled = ReproModeStateNotStarted;
                        break;

                    case ReproModeStateStarted:
                    default:
                        break;
                }
            }
            break;  

        case EVENT_CONTROL_CODE_DISABLE_PROVIDER:
            if (g_eReproModeLoggingEnabled == ReproModeStateStarted) 
            {
                // 
                // Merge verbose firmware logs into ETW log (if not done already).
                // Disable verbose firmware logs
                // 
                g_eReproModeLoggingEnabled = ReproModeStateNotStarted;
            }
            break;

        case EVENT_CONTROL_CODE_CAPTURE_STATE:
            if (Level == IHV_ETW_REPRO_MODE_LEVEL &&
                g_eReproModeLoggingEnabled == ReproModeStateStarted)
            {
                // 
                // Merge verbose firmware logs into ETW log (if not done already).
                // Disable verbose firmware logs
                // 
                g_eReproModeLoggingEnabled = ReproModeStateCaptured;
            }
            break;  
    }
}
```

## <a name="testing-the-repro-mode-logs"></a>测试重现模式日志

若要测试 IHV 重现模式日志，可以使用以下命令来启动和停止捕获。 

> [!NOTE]
> 生成的 ETL 文件将包含某些 OS 日志。

- netsh wlan IHV startlogging
- netsh wlan IHV stoplogging

客户也使用这些命令手动从设备收集日志。

## <a name="submitting-ihv-providers-to-microsoft"></a>提交给 Microsoft 的 IHV 提供程序

Ihv 提交重现模式用户启动反馈的最后一步是为与 Microsoft 联系，并提供请求的提供程序 Guid、 级别和标志以及示例日志数据以供审核。 日志记录经过审批后，提供程序将添加到用户启动的反馈系统中。 

> [!NOTE]
> 对提供程序 Guid、 级别或标志后提交不会影响 UIF 日志进行任何修改。

## <a name="related-links"></a>相关链接

[用户启动使用 IHV 跟踪日志记录的反馈](user-initiated-feedback-with-ihv-trace-logging.md)

[用户启动的反馈-正常模式](user-initiated-feedback-normal-mode.md)
