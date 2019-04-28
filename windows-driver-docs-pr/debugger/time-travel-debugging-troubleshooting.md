---
title: 时光穿越调试 - 故障排除
description: 本部分介绍如何进行故障排除时传输跟踪。
ms.date: 10/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9fcb1c922b3bc769d78153c0fb90c01f31be67f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349023"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---troubleshooting"></a>时光穿越调试 - 故障排除

本部分介绍如何进行故障排除时传输跟踪。

## <a name="issues-attempting-to-record-a-process"></a>尝试记录过程的问题

### <a name="i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>我收到错误消息，指出"WinDbg 必须运行提升的权限以支持时间旅行调试"

该消息指示，如运行提升的调试器是一项要求。 若要运行提升的调试器，右键单击**WinDbg 预览版**图标，在开始菜单，然后选择**详细** > **以管理员身份运行**。

### <a name="i-installed-windbg-preview-with-an-account-that-does-not-have-administrator-privileges-and-i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>我不具有管理员权限的帐户安装 WinDbg 预览版，我收到错误消息，指出"WinDbg 必须运行提升的权限以支持时间旅行调试"

重新安装使用的帐户具有管理员权限的 WinDbg 预览并记录在调试器中时使用该帐户。

### <a name="i-cant-launch-and-record-a-uwp-application"></a>无法启动并记录的 UWP 应用程序

在此期间，不支持此但可能会将附加到并记录已在运行 UWP 应用程序。

### <a name="i-cant-record-a-insert-name-of-unusual-process-type---running-in-another-session-security-context-credentials-process"></a>我无法录制 < 插入的不寻常的进程类型-运行在另一个会话、 安全上下文、 凭据名称...> 进程

在此期间，TTD 仅记录正则启动的进程，您可以将通常从命令控制台或通过单击可执行文件或快捷方式在 Windows 资源管理器。

### <a name="i-cannot-successfully-record-my-application-on-my-computer"></a>我无法成功录制我的计算机上的我的应用程序

如果录制你的应用程序失败，请验证您可以记录简单的 Windows 进程。  例如，"ping.exe"或"cmd.exe"是通常情况下可以记录的简单过程。

### <a name="i-cannot-successfully-record-anything-at-all-on-my-computer"></a>我就不能成功根本记录任何内容，我的计算机上

TTD 录制已侵入性的技术，这会干扰其他侵入性技术，如应用程序虚拟化框架、 信息管理产品、 安全软件或防病毒产品。

请参阅中的"时要注意的事物"[时间旅行调试-概述](time-travel-debugging-overview.md)有关已知 TTD 不兼容问题的信息。

### <a name="im-tracing-an-application-and-running-appverifer-at-the-same-time-and-the-performance-when-replaying-the-trace-is-slow"></a>我是跟踪应用程序，在同一时间运行 AppVerifer 和重播跟踪时性能不佳。

由于方式 AppVerifer 使用内存来重播跟踪可以明显不如而无需 AppVerifier 检查应用程序，体验更高版本。 若要提高性能，禁用 AppVerifier 记录应用程序时。 如果无法做到这一点，您可能需要关闭以提高性能的 WinDbg 中的调用堆栈窗口。


## <a name="issues-with-idx-index-files"></a>问题。IDX 索引文件

调试跟踪文件没有索引文件，或已损坏或不完整的索引文件，是可能的但不是建议。
需要确保内存使用索引文件从调试的进程读取的值是最准确的并提高效率的所有其他调试操作。

使用`!index -status`命令检查的状态。与关联的 IDX 索引文件。运行跟踪文件。

如果它您可以尝试重新创建索引文件通过运行`!index -force`。

### <a name="recreating-the-idx-index-file"></a>重新创建。IDX 索引文件

如果您怀疑，即使索引文件后，发出或`!index -status`所讲的内容不是"Index 加载文件"，重新创建它。
若要这样做可能会运行`!index -force`。 如果该操作失败：

1. 关闭调试器。
2. 删除现有 IDX 文件，它将具有相同的名称。运行跟踪文件，并位于同一目录中的。运行的文件。
3. 打开跟踪。运行 WinDbg 预览版中的文件。 这将运行`!index`命令以重新创建该索引。
4. 使用`!index -status`命令，确认该跟踪索引可正常运行。

确保有足够的空间用于跟踪文件所在的同一位置中的索引文件。
具体取决于该录制的内容，索引文件可能会显著大于跟踪文件，通常约为两次尽可能大。

## <a name="issues-with-trace-run-files"></a>跟踪的问题。运行文件

问题跟踪时。运行文件，可能会收到如下错误消息。

```dbgcmd
Replay and log are out of sync at fallback data. Packet type is incorrect "Packet Type"
Replay and log are out of sync at opaque data. Log had already reached the end
Replay exit thread event does not match up with logged event
Logged debug write values are out of sync with replay
```

在大多数情况下的所有失败消息，指示。运行的跟踪文件不可用，并且必须重新录制。


### <a name="re-recording-the-user-mode-app"></a>重新录制用户模式应用程序

如果没有录制用户模式应用程序的特定问题，可能想要尝试录制在同一台 PC 上的不同应用或尝试不同的 PC 上的相同应用。 您可能想要尝试并记录使用不同的应用程序以查看是否存在记录应用程序的某些部分的特定问题。


### <a name="when-debugging-or-creating-the-index-i-see-messages-about-derailment-events"></a>当调试或创建索引时，我看到有关"Derailment 事件"的消息。

此外，可以，你可能会看到如下消息：

```dbgcmd
Derailment event MissingDataDerailment(7) on UTID 2, position 2A550B:108 with PC 0x7FFE5EEB4448 Request address: 0x600020, size: 32
```

TTD 工作原理是运行仿真程序内执行的调试进程才能复制该过程中记录每个位置处的状态的说明进行操作，调试程序。 此仿真器观察到某种形式的结果状态和跟踪文件中的信息之间的差异时，会发生正轨。 例如，带引号的更高版本，该错误是指 0x7FFE5EEB4448，位置跟踪尝试读取不存在录制中的位置 0x600020，围绕一些内存内容中的位置 2A550B:108 中找到的指令。

正轨通常由某些错误中录制器，或有时在模拟器中，某些录制的指令处进一步在跟踪中返回。 

在大多数情况下此失败消息指示的。运行的跟踪文件将具有正常执行，它正常执行的一些不确定的指令数的点处开始的线程中存在间隔。 如果你尝试调试的感兴趣的事件并未发生期间的差距，跟踪可能可用。 如果感兴趣的事件发生期间的差距，跟踪将需要重新录制。


## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---






