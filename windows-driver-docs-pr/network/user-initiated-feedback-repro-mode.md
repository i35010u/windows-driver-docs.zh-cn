---
title: 用户发起的反馈 - 再现模式
description: 本主题介绍在 WDI 驱动程序中通过 IHV 跟踪日志记录执行用户启动的反馈的重现模式。
ms.date: 06/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 320ad9460f974b2b855da7ae3ba86e1d730de2ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805149"
---
# <a name="user-initiated-feedback---repro-mode"></a>用户发起的反馈 - 再现模式

用户启动的反馈 (UIF) 重现模式允许系统在用户重现 bug 时收集更详细的日志记录。 与 UIF normal 模式一样，这也是通过使用 IHV 定义的 ETW 提供程序创建新的 WMI 日志记录会话来实现的。 在重现模式完成后，将收集详细日志并将其发送给 Microsoft 进行分析。 存在用于启用或禁用详细固件日志的 IHV 扩展点。 重现日志旨在更详细地跟踪客户遇到问题的原因。） 因此，重现模式日志的日志文件大小设置为最大大小为10MB。 IHV 应为 ETW 提供程序标志/级别/关键字值使用更详细的设置。

当前 UIF 重现模式模型要求在包含 IHV 反馈日志之前，向 Microsoft 通知所有提供程序 Guid、级别和标志。 如本主题中所述，向注册表中添加提供程序可使 IHV 测试日志以获取适当的级别。

## <a name="microsoft-provided-wmi-auto-logger-session"></a>Microsoft 提供的 WMI 自动记录器会话

Microsoft 提供了不带初始 ETW 提供程序的 WMI 自动记录器会话。 安装 IHV 的驱动程序时，必须在 Microsoft 提供的 WMI 自动记录器会话密钥下添加所需的 WMI 提供程序注册表项。 IHV 不应更改任何自动记录器会话注册表值。 但是，所有 ETW 提供程序选项都可用于 IHV，包括 enable level、match any、match all 等。

> [!IMPORTANT]
> 永远不会将自动记录器启用为自动记录器。 这些值用于验证 [测试重现模式日志](#testing-the-repro-mode-logs)中所述的重现模式 IHV 日志记录。 此外，我们可能会要求用户使用工具手动提交这些日志 `netsh` 。 提供程序 Guid、级别和标志还必须提交给 Microsoft，以及日志的示例，因此它们将包含在重现模式下 UIFs (参阅将 [IHV 提供程序提交给 Microsoft](#submitting-ihv-providers-to-microsoft)。

WMI 自动记录器会话已添加到具有以下路径的 HKLM 注册表配置单元：

`HKLM,SYSTEM\CurrentControlSet\Control\WMI\Autologger\WifiDriverIHVSessionRepro`

生成的 ETL 日志文件位于以下位置：

`%SystemDrive%\System32\LogFiles\WMI\WifiDriverIHVSessionRepro.etl`

## <a name="ihv-driver-inf-changes"></a>IHV 驱动程序 INF 更改

Ihv 需要更新其驱动程序 INF 文件来添加以下注册表项值，以便它们可以在 UIF 正常模式下获取详细的 IHV 日志。 以下代码片段提供了用于将单个 ETW 提供程序添加到自动记录器会话的模板。 IHV 可以添加尽可能多的提供程序。 此外，每个 ETW 提供程序的启用级别值都是特定于 IHV 的，因此它们不必与 Microsoft 定义的值相同 (TRACE_LEVEL_CRITICAL、TRACE_LEVEL_ERROR 等 ) 。

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

此示例显示了 WDI UE 信息级别设置和所有关键字：

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

## <a name="etw-control-callback"></a>ETW 控件回调

IHV 可以在其 ETW 日志记录代码中注册 ETW 控制回调。 这使 IHV 在启用、禁用 ETW 提供程序或启动捕获控件时得到通知。 这样，IHV 就可以打开或关闭用于重现模式的详细固件日志。

> [!NOTE]
> 如果 ETW 提供程序在正常和重现模式间共享，则 IHV 应关闭 INF 文件中定义的由 IHV 定义的 EnableLevel，以启动/停止详细固件日志。

### <a name="etw-callback-function"></a>ETW 回调函数

下面的代码片段演示如何注册 ETW 回调。 这仅在以下情况下才重要： IHV 需要在 UIF 重现模式开始和结束期间采取特殊措施 (如启动或停止详细固件日志记录) 。 如果使用多个 ETW 提供程序，则 Ihv 可能只考虑实现一个回调来启动固件日志记录。 所有固件日志记录都必须路由到 IHV 的 ETW 跟踪提供程序。 UIF 的诊断工具将只收集 IHV 的 ETW 提供程序的跟踪。

可以通过两种方法启用 ETW 回调，具体取决于你实现 ETW 日志记录的方式。

1. 通过自动生成的代码 ETWs 的清单 `MC.exe` 。 请参阅 [编写检测清单](/windows/desktop/WES/writing-an-instrumentation-manifest) 了解更多详细信息。
    1. 以下代码片段中的标头 (etwtracingevents) 是通过创建的自动生成的 ETW 事件标头 `MC.exe` 。 假定已经生成了 ETW 事件，因此本主题并不关注此部分。
    1. 必须先定义 MCGEN_PRIVATE_ENABLE_CALLBACK_V2，然后才能包含自动生成的 ETW 标头。 否则，将不会调用该回调。
1. 通过 [**EventRegister**](/windows/win32/api/evntprov/nf-evntprov-eventregister) API 注册 ETW 回调。
    1. 注册跟踪提供程序时，必须将 ETW 回调提供程序传递到 **EventRegister** 函数。

此代码片段显示了 ETW 回调函数的原型。

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

仅当使用工具自动生成 ETW 事件时，才需要以下代码 `MC.exe` 。

```C++
#define MCGEN_PRIVATE_ENABLE_CALLBACK_V2 EtwEventControlCallback

#include "etwtracingEvents.h" // Generated from manifest - This must come 
                              // after MCGEN_PRIVATE_ENABLE_CALLBACK_V2 is                   
                              // defined
```

ETW 回调的 *ControlCode* 参数指示何时启用或禁用该提供程序。 值在中定义 `<evntrace.h>` ，并且具有以下值：

```C++
#define EVENT_CONTROL_CODE_DISABLE_PROVIDER 0
#define EVENT_CONTROL_CODE_ENABLE_PROVIDER  1
#define EVENT_CONTROL_CODE_CAPTURE_STATE    2
```

#### <a name="event_control_code_enable_provider"></a>EVENT_CONTROL_CODE_ENABLE_PROVIDER

此标志启用 ETW 提供程序，并指示 UIF 重现模式会话已启动。 这应该用于启动详细的固件日志记录和/或数据包日志记录。

#### <a name="event_control_code_disable_provider"></a>EVENT_CONTROL_CODE_DISABLE_PROVIDER

此标志禁用 ETW 提供程序，并指示 UIF 重现模式会话已结束。 如果 *级别* 参数与以下部分的示例)  (0xff 中的 INF 文件中的 IHV 指定的 UIF 重现模式级别匹配，则 IHV 的实现应在此时刷新和重置固件日志。

#### <a name="event_control_code_capture_state"></a>EVENT_CONTROL_CODE_CAPTURE_STATE

此标志请求提供程序记录其状态信息。 通常会调用此，将内存中的日志刷新到磁盘。 如果 *级别* 参数与以下部分的示例)  (0xff 中的 INF 文件中的 IHV 指定的 UIF 重现模式级别匹配，则 IHV 的实现应在此时刷新和重置固件日志。

### <a name="sample-code"></a>示例代码

下面是一个示例 ETW 回调实现，可将其用作模板，以便为 UIF 重现模式方案启用详细驱动程序和固件日志记录。

> [!NOTE]
> Ihv 需要刷新 **EVENT_CONTROL_CODE_CAPTURE_STATE** 和 **EVENT_CONTROL_CODE_DISABLE_PROVIDER** 控制代码的任何挂起的固件日志。

调用 **EVENT_CONTROL_CODE_CAPTURE_STATE** 后，UIF 诊断工具将多次调用 ETW 回调，并提供 **EVENT_CONTROL_CODE_ENABLE_PROVIDER** 控制代码。 因此，为了避免重新启用固件日志记录，状态机将从 *ReproModeStateCaptured* 状态移动到 *ReproModeStateFinal* 状态，然后再移回到 *ReproModeStateNotStarted* 状态。 **EVENT_CONTROL_CODE_DISABLE_PROVIDER** 控制代码仅用于禁用该提供程序。 这不是 UIF 过程的一部分，但仍需遵守。

Ihv 应更改以下示例中的 **IHV_ETW_REPRO_MODE_LEVEL** 值，以匹配 INF 文件中设置的重现模式级别。

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

客户还可以使用这些命令从设备中手动收集日志。

## <a name="submitting-ihv-providers-to-microsoft"></a>将 IHV 提供程序提交给 Microsoft

Ihv 提交重现模式用户启动的反馈的最后一步是与 Microsoft 联系，并提供所请求的提供程序 Guid、级别和标志以及用于评审的示例日志数据。 审核日志记录后，将向用户启动的反馈系统添加提供程序。 

> [!NOTE]
> 提交后对提供程序 Guid、级别或标志的任何修改都不会对 UIF 日志产生任何影响。

## <a name="related-links"></a>相关链接

[用户使用 IHV 跟踪日志记录发起的反馈](user-initiated-feedback-with-ihv-trace-logging.md)

[用户发起的反馈 - 正常模式](user-initiated-feedback-normal-mode.md)
