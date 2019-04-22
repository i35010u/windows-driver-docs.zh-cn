---
title: Bug 检查 0xEF CRITICAL_PROCESS_DIED
description: CRITICAL_PROCESS_DIED bug 检查具有 0x000000EF 值。 这表示关键系统进程死了。
ms.assetid: caa18221-6128-4d77-ab61-ef3c28cfba38
keywords:
- （开发人员内容）Bug 检查 0xEF CRITICAL_PROCESS_DIED
- CRITICAL_PROCESS_DIED
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- CRITICAL_PROCESS_DIED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cf9157bb026289226aa5e1ab54bb47825bc79ee7
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239622"
---
# <a name="developer-content-bug-check-0xef-criticalprocessdied"></a>（开发人员内容）Bug 检查 0xEF:关键\_进程\_DIED

CRITICAL_PROCESS_DIED bug 检查具有 0x000000EF 值。 这表示关键系统进程死了。 关键进程是一个 bug 检查强制系统，如果其终止。 这可能发生时的进程状态已损坏或否则已损坏。 在此情况下，因为这些进程是 Windows 正常运行至关重要，检查系统错误时发生操作系统完整性。 

构建在 Windows 中关键系统服务包括 csrss.exe、 wininit.exe，logonui.exe、 smss.exe、 services.exe、 conhost.exe 和 winlogon.exe。 

开发人员还可以创建一个服务和一组其恢复选项以重新启动计算机的详细信息，请参阅[设置到需要位置时服务出现故障的恢复操作](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753662(v=ws.11))。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="criticalprocessdied-parameters"></a>关键\_进程\_DIED 参数


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
<td align="left"><p>进程对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>如果这是 0，已中止进程。 如果这是 1，已中止线程。</p></td>
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

 

<a name="resolution"></a>分辨率
----------

确定导致此问题通常需要使用调试器以收集其他信息。 应检查多个转储文件，以查看此停止代码是否具有类似特征，例如停止代码出现时运行的代码。

有关详细信息，请参阅[使用 Windows 调试器 (WinDbg) 的故障转储分析](crash-dump-files.md)， [Using ！ 分析扩展](using-the--analyze-extension.md)并[！ 分析](-analyze.md)。

在许多情况下用户转储还会创建之前系统错误检查。  一般情况下，当用户转储不可用，它应进行检查，第一次根本原因问题。 这是因为调试从内核转储，包括分页的扩展/缺少的数据在用户模式代码有限制。 有关详细信息，请参阅[用户模式转储文件](user-mode-dump-files.md)。 

请考虑使用事件日志以查看是否存在此停止代码导致发生的错误。 如果有，这些错误可用于检查特定的服务或其他代码进行调查。

如果随意，可重现的 bug 检查，请考虑使用时间旅行跟踪记录的事件导致的 bug 检查。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。

有关代码有问题的信息可用后，相关代码中设置断点之前这段代码执行和单个向前迈出了通过查看用于控制代码流的关键变量的值的代码。  仔细检查您的代码以查找错误的假设或其他错误的此区域。 

使用错误检查的第二个参数来确定中断进程或线程导致的 bug 检查。

如果它是一个过程，使用[！ 过程](-process.md)命令之前和之后要查找异常行为的故障点的过程中显示的信息。 [进程资源管理器](https://docs.microsoft.com/sysinternals/downloads/process-explorer)实用工具可以用于收集有关哪个进程是否正在运行以及父子关系的常规信息。

如果它是一个线程，请考虑使用[！ 线程](-thread.md)命令以显示有关线程的信息。 有关内核模式中的线程的信息，请参阅[更改上下文](changing-contexts.md)。 

有关线程和进程的常规信息，以及 Windows 保护，例如 wininit 和 csrss，关键代码的其他详细信息请参阅*Windows 内部结构*通过 Pavel Yosifovich、 Mark E.Russinovich、 David A.Solomon 和 AlexIonescu。



**常规疑难解答提示**

如果您不能使用调试器，这些常规故障排除提示可能会有帮助。

-   如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

-   如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   请与制造商联系，以查看更新的系统 BIOS 或固件是否可用。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   运行病毒检测程序。 病毒可能会感染所有类型的 for Windows，格式化的硬盘，并生成磁盘损坏可生成系统 bug 检查代码。 请确保病毒检测程序会检查存在感染主启动记录。

-   使用系统文件检查器工具来修复丢失或损坏系统文件。 系统文件检查器是一个实用程序允许用户在 Windows 系统文件损坏扫描和还原 Windows 中的损坏的文件。 使用以下命令运行系统文件检查器 (SFC.exe)。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用的系统文件检查器工具来修复丢失或损坏系统文件](https://support.microsoft.com/kb/929833)。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

 

 




