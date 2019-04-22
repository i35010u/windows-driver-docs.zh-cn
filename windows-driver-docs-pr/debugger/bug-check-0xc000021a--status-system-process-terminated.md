---
title: Bug 检查 0xC000021A STATUS_SYSTEM_PROCESS_TERMINATED
description: STATUS_SYSTEM_PROCESS_TERMINATED bug 检查具有 0xC000021A 值。 这意味着，出现错误的用户模式的关键子系统中。
ms.assetid: d46e2948-ff18-49e0-a738-7b90ab54d333
keywords:
- Bug 检查 0xC000021A STATUS_SYSTEM_PROCESS_TERMINATED
- STATUS_SYSTEM_PROCESS_TERMINATED
ms.date: 03/15/2019
topic_type:
- apiref
api_name:
- STATUS_SYSTEM_PROCESS_TERMINATED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b19f8db5152c9fdb7a8265216ce8148c7e73330d
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239170"
---
# <a name="bug-check-0xc000021a-statussystemprocessterminated"></a>Bug 检查 0xC000021A：状态\_系统\_进程\_已终止


状态\_系统\_进程\_TERMINATED bug 检查的值为 0xC000021A。 这意味着，出现错误的用户模式的关键子系统中。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="statussystemprocessterminated-parameters"></a>状态\_系统\_进程\_TERMINATED 参数


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
<td align="left"><p>一个字符串，标识问题</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误代码</p></td>
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

 

<a name="cause"></a>原因
-----

在用户模式下的子系统，例如 WinLogon 或客户端服务器运行时子系统 (CSRSS)，已遭到严重破坏，无法再保证安全时，将发生此错误。 在响应中，操作系统将切换到内核模式。 Microsoft Windows 不能运行而无需 WinLogon 或 CSRSS。 因此，这是一个用户模式服务的失败可以关闭系统的几个用例。

不匹配的系统文件也会导致此错误。 如果从备份中还原您的硬盘，这可能发生。 某些备份程序可能会跳过还原它们确定正在使用的系统文件。

<a name="resolution"></a>分辨率
----------

运行内核调试程序可能无法在此情况下有用因为实际错误发生在用户模式进程中。

**解决用户模式设备驱动程序、 系统服务或第三方应用程序中的错误：** 因为用户模式进程中发生 bug 检查 0xC000021A，最常见的原因是第三方应用程序。 如果错误发生在新的或更新设备驱动程序、 系统服务或第三方应用程序的安装后，新的软件应该删除或禁用，以找出原因。 有关可能的更新的软件制造商联系。

**解决的不匹配的系统文件的问题：** 如果你最近已从备份还原您的硬盘，检查是否有备份/还原计划的更新的版本可从制造商。

这些步骤中收集的其他信息可能会有所帮助。

-   查看最新安装的应用程序。 若要执行此操作导航到"卸载或更改程序"控制面板和排序中安装的应用程序的安装日期。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

<a name="remarks"></a>备注
----------

这些步骤可能有助于解决此问题。

-   使用系统文件检查器工具来修复丢失或损坏系统文件。 系统文件检查器是一个实用程序允许用户在 Windows 系统文件损坏扫描和还原 Windows 中的损坏的文件。 使用以下命令运行系统文件检查器 (SFC.exe)。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用的系统文件检查器工具来修复丢失或损坏系统文件](https://support.microsoft.com/kb/929833)。

-   运行病毒检测程序。 病毒可能会感染所有类型的 for Windows，格式化的硬盘，并生成磁盘损坏可生成系统 bug 检查代码。 请确保病毒检测程序会检查存在感染主启动记录。

-   验证系统安装了最新 Service Pack。 若要检测的 Service Pack，如果任何，安装在您的系统上，单击**启动**，单击**运行**，类型**winver**，然后按 ENTER。 **有关 Windows**对话框中显示 Windows 版本号和版本号的 Service Pack，如果安装一个。

**使用安全模式**

请考虑使用安全模式相隔离以进行故障排除的元素，如有必要，若要使用 Windows。 使用安全模式下加载的最小所需的驱动程序和系统服务在 Windows 启动过程。 若要进入安全模式下，使用**更新和安全**设置中。 选择**恢复**-&gt;**高级启动**启动到维护模式。 在生成菜单中选择**进行故障排除**- &gt; **高级选项** - &gt; **启动设置** - &gt; **重新启动**。 Windows 重新启动到后**启动设置**屏幕上，选择选项 4、 5 或 6 到安全模式下启动。

安全模式下可通过按功能键上启动，例如 F8。 请参阅信息从制造商为特定的启动选项。

 

 




