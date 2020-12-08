---
title: Bug 检查 0xC000021A WINLOGON_FATAL_ERROR
description: WINLOGON_FATAL_ERROR bug 检查的值为0xC000021A。 这意味着 Winlogon 进程意外终止。
keywords:
- Bug 检查 0xC000021A WINLOGON_FATAL_ERROR
- WINLOGON_FATAL_ERROR
ms.date: 09/12/2019
topic_type:
- apiref
api_name:
- WINLOGON_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75b4f51d3d3a29fe6a5c54473fb570d97920bc4b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813993"
---
# <a name="bug-check-0xc000021a-winlogon_fatal_error"></a>Bug 检查0xC000021A： WINLOGON \_ 严重 \_ 错误

WINLOGON \_ \_ 错误错误检查的值为0xc000021a。 这意味着 Winlogon 进程意外终止。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="winlogon_fatal_error-parameters"></a>WINLOGON \_ 严重 \_ 错误参数

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>用于标识问题的字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>错误代码</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

当 (CSRSS) 的用户模式子系统 Run-Time 子系统已严重安全，无法再保证安全时，会发生此错误。 在响应中，操作系统切换到内核模式。 Microsoft Windows 无法在没有 WinLogon 或 CSRSS 的情况下运行。 因此，在这种情况下，用户模式服务的故障可能会关闭系统。

系统文件不匹配也可能导致此错误。 如果从备份还原了硬盘，则会出现这种不匹配情况。 某些备份程序可能会跳过还原其确定正在使用的系统文件。

<a name="resolution"></a>解决方法
----------

运行内核调试器在这种情况下可能不起作用，因为用户模式进程中发生了实际错误。

### <a name="resolving-an-error-in-a-user-mode-device-driver-system-service-or-third-party-application"></a>解决用户模式设备驱动程序、系统服务或第三方应用程序中的错误

由于 bug 检查0xC000021A 发生在用户模式进程中，最常见的原因是第三方应用程序。 如果在安装新的或更新的设备驱动程序、系统服务或第三方应用程序之后出现错误，则应删除或禁用新软件以找出原因。 有关可能的更新，请与软件制造商联系。

### <a name="resolving-a-mismatched-system-file-problem"></a>解决不匹配的系统文件问题

如果最近从备份还原了硬盘，请检查制造商是否有可用的备份/还原程序的更新版本。

- 查看最近安装的应用程序。 要执行此操作，请导航到控制面板中的 "卸载或更改程序"，并按安装日期对已安装的应用程序进行排序。

- 检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在系统日志中查找与蓝屏同时出现的严重错误。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 在系统日志中查找与蓝屏同时出现的严重错误。

<a name="remarks"></a>备注
-------

- 使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令 ( # A0) 运行系统文件检查器工具。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

-   运行病毒检测程序。 病毒可能会感染格式化为 Windows 的所有类型的硬盘，并且生成的磁盘损坏可以生成系统 bug 检查代码。 请确保病毒检测程序检查主启动记录中是否有病毒感染。

-   验证系统是否安装了最新更新。 若要检测系统上安装的版本，请选择 " **开始**"，选择 " **运行**"，键入 **winver**，然后按 enter。 如果已安装) ，则 " **关于 windows** " 对话框将显示 Windows 版本号 (和 Service Pack 的版本号。

### <a name="using-safe-mode"></a>使用安全模式

请考虑使用安全模式隔离元素以便进行故障排除，并在必要时使用 Windows。 使用安全模式仅加载 Windows 启动过程中所需的最少驱动程序和系统服务。

若要进入安全模式，请使用 "设置" 中的 " **更新和安全** "。 选择 "**恢复** &nbsp; &gt; **高级启动**" 以启动到维护模式。 在出现的菜单中，**选择 "** &nbsp; &gt; **高级选项**" "启动 &nbsp; &gt; **设置** &nbsp; &gt; **重新启动**"。 在 Windows 重新启动并显示 " **启动设置** " 屏幕后，选择选项4、5或6启动到安全模式。

安全模式也可通过在启动时按功能键来提供，例如 F8。 请参阅计算机制造商提供的有关特定启动选项的信息。
