---
title: 时光穿越调试 - 故障排除
description: 本部分介绍如何排查时间行程跟踪问题。
ms.date: 10/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: a454221b6e823a59a0a770f628378e10b13ee705
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916120"
---
# <a name="time-travel-debugging---troubleshooting"></a>时光穿越调试 - 故障排除

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png) 

本部分介绍如何排查时间行程跟踪问题。

## <a name="issues-attempting-to-record-a-process"></a>尝试记录进程时出现问题

### <a name="i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>我收到一条错误消息，显示 "WinDbg 必须提升到支持时间来进行行程调试"

正如消息中所指示的，运行提升调试器是一个要求。 若要以提升的权限运行调试器，请右键单击 "开始" 菜单中的 " **WinDbg 预览**" 图标，然后选择 "**更多** > 以**管理员身份运行**"。

### <a name="i-installed-windbg-preview-with-an-account-that-does-not-have-administrator-privileges-and-i-get-an-error-message-that-says-windbg-must-be-run-elevated-to-support-time-travel-debugging"></a>我使用不具有管理员权限的帐户安装了 WinDbg 预览版，并收到一条错误消息，显示 "WinDbg 必须提升以支持时间来进行旅行调试"

使用具有管理员权限的帐户重新安装 WinDbg 预览版，并在调试器中记录时使用该帐户。

### <a name="i-cant-launch-and-record-a-uwp-application"></a>无法启动和录制 UWP 应用程序

此时不支持这种情况，但你可以附加到并记录已运行的 UWP 应用程序。

### <a name="i-cant-record-a-insert-name-of-unusual-process-type---running-in-another-session-security-context-credentials-process"></a>我无法记录 < 不正常的进程类型的插入名称-在另一个会话中运行，安全上下文，凭据 .。。> 进程

此时，TTD 仅记录通常可以从命令控制台启动的定期进程，或者单击 Windows 资源管理器中的可执行文件或快捷方式。

### <a name="i-cannot-successfully-record-my-application-on-my-computer"></a>我无法在我的计算机上成功记录我的应用程序

如果你的应用程序的记录失败，请验证你是否可以记录一个简单的 Windows 进程。  例如，"dism.exe" 或 "cmd.exe" 是通常可以记录的简单过程。

### <a name="i-cannot-successfully-record-anything-at-all-on-my-computer"></a>我无法在我的计算机上成功地记录所有内容

TTD 记录是一种侵害性技术，它可能会干扰应用程序虚拟化框架、信息管理产品、安全软件或防病毒产品等其他侵害性技术。

请参阅[行程调试](time-travel-debugging-overview.md)中的 "要注意的内容"-有关已知 TTD 不兼容信息的概述。

### <a name="im-tracing-an-application-and-running-appverifer-at-the-same-time-and-the-performance-when-replaying-the-trace-is-slow"></a>我同时跟踪应用程序并运行 AppVerifer，并且重播跟踪时的性能会很慢。

由于 AppVerifer 使用内存来检查应用程序的方式，因此，重播跟踪时的体验会明显比不使用 AppVerifier 更糟。 若要提高性能，请在记录应用时禁用 AppVerifier。 如果这是不可能的，则可能需要关闭 WinDbg 中的调用堆栈窗口，以提高性能。


## <a name="issues-with-idx-index-files"></a>有关的问题。IDX 索引文件

可以不使用索引文件或已损坏或不完整的索引文件调试跟踪文件，但不建议这样做。
需要索引文件，以确保从调试的进程读取的内存值最为准确，并提高所有其他调试操作的效率。

使用 `!index -status` 命令来检查的状态。与关联的 IDX 索引文件。运行跟踪文件。

如果可以尝试通过运行 `!index -force`重新创建索引文件。

### <a name="recreating-the-idx-index-file"></a>重新创建。IDX 索引文件

如果怀疑索引文件有问题，或者 `!index -status` 说 "加载的索引文件" 之外的任何内容，请重新创建该文件。
为此，可以运行 `!index -force`。 如果失败：

1. 关闭调试器。
2. 删除现有的 IDX 文件，它将具有与相同的名称。运行跟踪文件，并将其放在与相同的目录中。运行文件为。
3. 打开跟踪。在 WinDbg Preview 中运行文件。 这将运行 `!index` 命令来重新创建索引。
4. 使用 `!index -status` 命令确认跟踪索引是否正常工作。

请确保索引文件在跟踪文件所在的同一位置有足够的空间。
根据记录的内容，索引文件可能比跟踪文件大很多，通常按两个大的顺序排列。

## <a name="issues-with-trace-run-files"></a>跟踪问题。运行文件

当跟踪出现问题时。运行文件时，可能会收到如下错误消息。

```dbgcmd
Replay and log are out of sync at fallback data. Packet type is incorrect "Packet Type"
Replay and log are out of sync at opaque data. Log had already reached the end
Replay exit thread event does not match up with logged event
Logged debug write values are out of sync with replay
```

大多数情况下，所有失败消息都指示。运行跟踪文件不可用，必须重新记录。


### <a name="re-recording-the-user-mode-app"></a>重新记录用户模式应用

如果在记录用户模式应用时出现特定问题，则可能要尝试在同一台电脑上记录不同的应用程序，或者在不同的 PC 上尝试使用同一应用程序。 你可能想要尝试并记录不同的应用程序使用情况，以查看记录应用程序的某些部分是否存在特定问题。


### <a name="when-debugging-or-creating-the-index-i-see-messages-about-derailment-events"></a>调试或创建索引时，显示有关 "Derailment 事件" 的消息。

可能会看到如下消息：

```dbgcmd
Derailment event MissingDataDerailment(7) on UTID 2, position 2A550B:108 with PC 0x7FFE5EEB4448 Request address: 0x600020, size: 32
```

TTD 的工作原理是在调试器内运行模拟器，这会执行已调试进程的指令，以便在记录中的每个位置复制该进程的状态。 当此模拟器在跟踪文件中发现产生的状态和信息之间的某种差异时，会发生 Derailments。 例如，上面提到的错误是指在位置0x7FFE5EEB4448 上找到的一个指令，该指令在跟踪中的位置2A550B：108，该指令尝试读取围绕位置0x600020 的一些内存，这在记录中不存在。

Derailments 通常是由记录器中的一些错误（有时也是在模拟器中）在跟踪中进一步返回的某些记录指令导致的。 

在大多数情况下，此失败消息表示。对于某些不确定的指令数，运行跟踪文件将在 derailed 的线程中有一个间隔，从它 derailed 的点开始。 如果尝试调试的感兴趣的事件未在该间隔期间发生，则可以使用该跟踪。 如果在此间隔期间发生了相关事件，则需要重新记录跟踪。


## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)

---






