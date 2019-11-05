---
title: DTrace ETW
description: DTrace 通过使用 LKD （）支持创建实时转储文件。
ms.assetid: bbf23d76-423d-4d1e-afde-83739015bbf1
keywords:
- DTrace WDK
- 软件跟踪 WDK，DTrace
- 显示跟踪消息
- 格式化跟踪消息 WDK DTrace
- 跟踪消息格式 WDK DTrace
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，DTrace
- 跟踪消息格式化文件 WDK
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: cb08888529dda9234e01e30bf765e1dca9c3f46d
ms.sourcegitcommit: 5081de283b09b4fe847912fc1dc0e7f057e0a0cd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73592427"
---
# <a name="dtrace-live-dump"></a>DTrace 实时转储

DTrace 提供一项功能，可使用 lkd （）从 D 脚本中捕获实时转储。 内存转储文件用于调试使用 Windows 调试器的 Windows 中的复杂问题。 有关详细信息，请参阅[使用 WinDbg 分析故障转储文件](https://docs.microsoft.com/windows-hardware/drivers/debugger/crash-dump-files)。 若要下载调试器，请参阅[WinDbg 预览-安装](https://docs.microsoft.com/windows-hardware/drivers/debugger/windbg-install-preview)。

 通过 DTrace 实时转储，可以在发生错误的确切位置触发转储。 例如，该错误可能是返回错误的函数。 当返回值为 "error" 时，可以使用 DTrace 挂钩到此函数返回并触发实时转储。

> [!NOTE]
> 版本18980和 Windows Server 有问必答 Preview 版本18975后，Windows 内部版本支持 DTrace。

有关在 Windows 上使用 DTrace 的常规信息，请参阅[dtrace](dtrace.md)。

## <a name="dtrace-live-dump-usage"></a>DTrace 实时转储使用情况

用法： **lkd （参数）;**

可以设置以下选项来更改实时迷你转储中包含的信息。

0x0-完整内核转储（默认值）

0x1-用户页面 + 内核页面（仅适用于 KD attach）

0x2-小型转储

0x4-Hyper-v 页面 + 内核页面）

0x5-用户、内核和虚拟机监控程序页面。

## <a name="live-dump-example-code"></a>实时转储示例代码

```dtrace
#pragma D option destructive

inline uint32_t STATUS_UNSUCCESSFUL = 0xc0000001UL;

syscall:::return
{ 
    this->status = (uint32_t)arg0;

    if (this->status == STATUS_UNSUCCESSFUL)
    { 
        printf ("Return value arg0:%x \n", this->status);
        printf ("Triggering LiveDump \n");
        lkd(0);
        exit(0);
    }
}
```

将该文件另存为 livedumpstatuscheck。

以管理员身份打开命令提示符，并使用-s 选项运行脚本。

```dtrace
C:\Windows\System32>dtrace -s livedumpstatuscheck.d
dtrace: script 'livedumpstatuscheck.d' matched 1881 probes
dtrace: allowing destructive actions
CPU     ID                    FUNCTION:NAME
  0     93 NtAlpcSendWaitReceivePort:return Return value arg0:c0000001
Triggering LiveDump
```

创建的转储文件通常位于 `C:\Windows\LiveKernelReports`。

如果转储文件的位置已更改，该值将存储在以下注册表项中： `hklm\system\currentcontrolset\control\crashcontrol\livekernelreports`

如上所述，使用 WinDbg 处理转储文件。

## <a name="troubleshooting"></a>“疑难解答”

### <a name="viewing-live-dump-related-events"></a>查看实时转储相关事件

打开 Windows 事件查看器：请参阅：应用程序和服务日志-> Microsoft > Windows-> Livedump-> 操作

如果找不到任何日志，请从命令提示符或事件查看器中启用分析通道，如下所述。

**通过命令提示符启用分析通道**

使用此命令从和管理员命令提示符启用分析通道。

`wevtutil sl Microsoft-Windows-Kernel-LiveDump/Analytic /e:true`

**使用事件查看器启用分析通道**

1. 启动 Windows 事件查看器

2. 单击 "查看"，然后选中 "显示分析和调试日志"。 这将显示 livedump 的分析通道。

3. 右键单击并启用 " *LiveDump/分析*"。

### <a name="enabling-full-live-dumps"></a>启用完整实时转储

下面的示例设置显示了在任意给定时间将磁盘上的最大完整实时转储数设置为10，并存储完整内存转储，而不只是小型转储。

`reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v FullLiveReportsMax /d 10`

`reg add "HKLM\System\CurrentControlSet\Control\CrashControl" /f /t REG_DWORD /v AlwaysKeepMemoryDump /d 1`

有关这些设置的详细信息，请参阅[WER 设置](https://docs.microsoft.com/windows/win32/wer/wer-settings)。

### <a name="disable-throttling"></a>禁用限制

限制是一项功能，阻止转储和日志记录系统影响 Windows 的正常使用。 此功能可能会影响某些资源约束环境中的实时转储创建。

检查实时转储限制设置，如果需要，请通过将 SystemThrottleThreshold 和 ComponentThrottleThreshold 键设置为零来禁用限制，如此处所示。

```registry
reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v SystemThrottleThreshold /d 0
reg add "HKLM\System\CurrentControlSet\Control\CrashControl\FullLiveKernelReports" /f /t REG_DWORD /v ComponentThrottleThreshold /d 0
```

### <a name="disk-space-issues-event-id-202--error-text-live-dump-write-deferred-dump-data-api-ended-nt-status-0xc000007f"></a>磁盘空间问题（事件 ID 202-错误文本：实时转储写入延迟转储数据 API 已结束。 NT 状态：0xC000007F。）

这意味着磁盘空间不足。 更新下面显示的注册表项，将实时转储的路径（在本示例中为驱动器 d：）更改为具有更多可用存储空间的驱动器 d：。

`reg add hklm\system\currentcontrolset\control\crashcontrol\livekernelreports /v "LiveKernelReportsPath" /t reg_sz /d "\??\d:\livedumps"`

此命令将实时转储根路径设置为 `d:\livedumps` （例如）。

不要手动创建该文件夹，因为它是由操作系统管理的，当使用适当的权限触发转储时，将创建该文件夹。

## <a name="see-also"></a>另请参阅

[Windows 上的 DTrace](dtrace.md)

[DTrace Windows 编程](dtrace-programming.md)

[DTrace Windows 代码示例](dtrace-code-samples.md)
