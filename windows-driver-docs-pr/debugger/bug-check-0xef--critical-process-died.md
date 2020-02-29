---
title: Bug 检查 0xEF CRITICAL_PROCESS_DIED
description: CRITICAL_PROCESS_DIED bug 检查的值为0x000000EF。 这表明关键系统进程终止。
ms.assetid: caa18221-6128-4d77-ab61-ef3c28cfba38
keywords:
- Bug 检查 0xEF CRITICAL_PROCESS_DIED
- CRITICAL_PROCESS_DIED
ms.date: 02/25/2020
topic_type:
- apiref
api_name:
- CRITICAL_PROCESS_DIED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 657ff1747b3830370b2ba5a976425cdd5dd1386b
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166669"
---
# <a name="bug-check-0xef-critical_process_died"></a>Bug 检查0xEF：严重\_进程\_终止

CRITICAL_PROCESS_DIED bug 检查的值为0x000000EF。 这表明关键系统进程终止。 关键过程是强制系统在终止时进行 bug 检查。 如果进程的状态已损坏或已损坏，则可能会发生这种情况。 发生这种情况时，由于这些进程对 Windows 的操作至关重要，因此系统 bug 检查发生的原因是操作系统的完整性。 

内置于 Windows 的关键系统服务包括 csrss、wininit、logonui、smss、、conhost 和 winlogon，等等）。

开发人员还可以创建服务，并设置其恢复选项以重新启动计算机。有关详细信息，请参阅[设置在服务失败时要执行的恢复操作](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753662(v=ws.11))。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="critical_process_died-parameters"></a>关键\_处理\_终止参数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>Process 对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果为0，则进程终止。 如果为1，则为线程终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>分辨率

确定此问题的原因通常需要使用调试器来收集其他信息。 应该检查多个转储文件，以查看此 stop 代码是否具有类似的特征，例如在出现停止代码时运行的代码。

有关详细信息，请参阅使用[！分析扩展](using-the--analyze-extension.md)和[！分析](-analyze.md)来[使用 Windows 调试器（WinDbg）进行故障转储分析](crash-dump-files.md)。

在许多情况下，还会在系统错误检查之前创建用户转储。  通常，当用户转储可用时，应该首先检查它的根本原因。 这是因为从内核转储调试用户模式代码有一些限制，包括取出/丢失数据。 有关详细信息，请参阅[用户模式转储文件](user-mode-dump-files.md)。 

请考虑使用事件日志来查看是否存在导致此停止代码的错误。 如果有，则可以使用这些错误来检查要调查的特定服务或其他代码。

如果有相关代码的信息可用，则在执行此代码之前，请在相关代码中设置一个断点，然后在代码中执行一步操作，以查看用于控制代码流的关键变量的值。  仔细检查代码区域，查找错误假设或其他错误。 

使用错误检查的第二个参数来确定中断进程或线程是否导致了 bug 检查。

如果它是一个进程，请使用[！ process](-process.md)命令显示故障点之前和之后的进程的信息，以查找异常行为。 [进程资源管理器](https://docs.microsoft.com/sysinternals/downloads/process-explorer)实用工具可用于收集有关正在运行的进程和父子关系的一般信息。

如果它是一个线程，请考虑使用[！ thread](-thread.md)命令显示有关该线程的信息。 有关内核模式下的线程的信息，请参阅[更改上下文](changing-contexts.md)。 

有关线程和过程的一般信息以及 Windows 保护的关键代码（如 wininit 和 csrss）的详细信息，请参阅*Windows 内部*Pavel Yosifovich、Mark Russinovich、David 和 Alex Ionescu。

## <a name="general-troubleshooting-tips"></a>常规疑难解答技巧

如果无法使用调试器，这些常规疑难解答提示可能会有所帮助。

-   如果最近向系统中添加了硬件，请尝试删除或替换它。 或与制造商联系，查看是否有可用的修补程序。

-   如果最近添加了新的设备驱动程序或系统服务，请尝试删除或更新它们。 尝试确定系统中发生了导致新 bug 检查代码的更改。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[Open 事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在与蓝色屏幕相同的时间范围内查找系统日志中的严重错误。

-   请与制造商联系，查看是否有更新的系统 BIOS 或固件可用。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   运行病毒检测程序。 病毒可能会感染为 Windows 格式化的所有类型的硬盘，导致磁盘损坏可能生成系统 bug 检查代码。 请确保病毒检测程序检查主启动记录中是否有病毒感染。

-   使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令运行系统文件检查器工具（SFC）。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

-   查看**设备管理器**，查看是否有任何设备标记为惊叹号（！）。 查看在驱动程序属性中显示的任何错误驱动程序的事件日志。 请尝试更新相关驱动程序。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅

[使用 Windows 调试器（WinDbg）进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)
