---
title: GFlags 详细信息
description: GFlags 详细信息
ms.assetid: 97faa63d-b876-4973-812f-f3bdd57c1778
keywords:
- GFlags、 详细信息
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: bfd6271b4f348b45da7899804b5338fc816449a2
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745872"
---
# <a name="gflags-details"></a>GFlags 详细信息

## <span id="ddk_gflags_details_dtools"></span><span id="DDK_GFLAGS_DETAILS_DTOOLS"></span>

GFlags 启用和禁用通过编辑 Windows 注册表和内部设置的系统功能。 本部分介绍 GFlags 的详细信息中的操作，并包括最有效地使用 GFlags 的技巧。

### <a name="span-idgeneralinformationspanspan-idgeneralinformationspangeneral-information"></a><span id="general_information"></span><span id="GENERAL_INFORMATION"></span>常规信息

- 若要显示 GFlags 对话框中，在命令行处，键入**gflags** （不带任何参数）。

- GFlags 系统级注册表设置在注册表中会立即显示，但直到重新启动系统不会生效。

- GFlags 图像文件注册表设置在注册表中会立即显示，但直到重新启动该进程不会生效。

- GFlags 对话框中的调试器和启动功能是特定的程序。 您可以仅设置其上一个图像文件一次。

### <a name="span-idflagdetailsspanspan-idflagdetailsspanflag-details"></a><span id="flag_details"></span><span id="FLAG_DETAILS"></span>标志的详细信息

- 若要清除所有标志，请将标志设置为-FFFFFFFF。 将标志设置为 0 将 0 添加到当前的标志值。

- Windows 将图像文件的标志设置为 FFFFFFFF (0xFFFFFFFF)，清除所有标志的图像文件，并删除**GlobalFlag**图像文件注册表项中的条目。 保留图像文件注册表项。

### <a name="span-iddialogboxandcommandlinespanspan-iddialogboxandcommandlinespandialog-box-and-command-line"></a><span id="dialog_box_and_command_line"></span><span id="DIALOG_BOX_AND_COMMAND_LINE"></span>对话框和命令行

可以通过使用其方便的对话框或命令行运行 GFlags。 大多数功能均可在两种形式，但存在以下例外。

**仅限对话框**

- 启动。 开始使用指定的标志的程序。

- 在调试器中运行程序。

- [特殊池](special-pool.md)Windows Vista 之前的系统上。 在 Windows Vista 和更高版本的 Windows 上，可以在命令行或 Gflags 对话框中配置特殊池功能。

**只有命令行**

- 设置的用户模式堆栈跟踪数据库大小 (/ tracedb)。

- 设置页面堆验证选项。

### <a name="span-idregistryinformationspanspan-idregistryinformationspanregistry-information"></a><span id="registry_information"></span><span id="REGISTRY_INFORMATION"></span>注册表信息

会话之间保存的 GFlags 设置存储在注册表中。 可以使用注册表 Api、 Regedit 中或 reg.exe 来查询或更改这些值。 下表列出了设置和注册表中存储的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>系统级设置 (&quot;注册表&quot;)</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\<strong>GlobalFlag</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>特定于程序的设置 (&quot;映像文件&quot;) 的计算机的所有用户。</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<em>映像文件名</em>\<strong>GlobalFlag</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>特定程序的无提示退出设置 (&quot;进程退出，无提示&quot;) 的计算机的所有用户。</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\<strong><em>ImageFileName</em></strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>计算机的所有用户的图像文件的页面堆选项</p></td>
<td align="left"><p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<em>映像文件名</em>\<strong>PageHeapFlags</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>用户模式堆栈跟踪数据库大小 (<strong>tracedb</strong>)</p></td>
<td align="left"><p>HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<em>映像文件名</em>\<strong>StackTraceDatabaseSizeInMb</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>创建用户模式堆栈跟踪数据库 (ust，0x1000) 的图像文件</p></td>
<td align="left"><p>Windows 将图像文件名称添加到 USTEnabled 注册表项的值 (HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<strong>USTEnabled</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在可能的情况下大型页加载映像</p></td>
<td align="left"><p>HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<em>映像文件名</em>\<strong>UseLargePages</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>特殊池</p>
<p>（内核特殊池标记）</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\<strong>PoolTag</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>验证开始/验证结束</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PoolTagOverruns. <strong>验证启动</strong>选项设置为 0 的值。 <strong>验证结束</strong>选项的值设置为 1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>图像文件的调试器</p></td>
<td align="left"><p>HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image 文件执行按<em>映像文件名</em>\<strong>调试器</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>对象引用跟踪</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Kernel\<strong>ObTraceProcessName</strong>, <strong>ObTracePermanent</strong> and <strong>ObTracePoolTags</strong></p></td>
</tr>
</tbody>
</table>
