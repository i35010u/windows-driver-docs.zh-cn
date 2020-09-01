---
title: 用户模式转储文件
description: 用户模式转储文件
ms.assetid: bef29d75-6620-4219-b402-36fbddc4fe1f
keywords:
- 转储文件，用户模式
ms.date: 12/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5803e913b3ccd4fd91044d67565545002426d154
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215686"
---
# <a name="user-mode-dump-files"></a>用户模式转储文件

本节包括：

- [各种用户模式转储文件](#varieties)

- [创建用户模式转储文件](#creating)

有关分析转储文件的信息，请参阅 [分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)。

## <a name="span-idvarietiesspanspan-idvarietiesspan-varieties-of-user-mode-dump-files"></a><span id="varieties"></span><span id="VARIETIES"></span> 各种用户模式转储文件

用户模式故障转储文件有多种，但分为两类：

[完全用户模式转储](#full)

[小型转储](#minidumps)

这些转储文件之间的差异是大小之一。 小型转储通常更紧凑，可轻松发送到分析师。

**注意**   可以通过分析转储文件来获取很多信息。 但是，任何转储文件都不能提供与实际使用调试器直接调试故障一样多的信息。

## <a name="span-idfullspanspan-idfullspanfull-user-mode-dumps"></a><span id="full"></span><span id="FULL"></span>完全用户模式转储

完整的用户 *模式转储* 是基本用户模式转储文件。

此转储文件包括进程的整个内存空间、程序的可执行文件映像本身、句柄表以及在重新构建转储时使用的内存时对调试器有用的其他信息。

可以将完整的用户模式转储文件 "收缩" 到小型转储。 只需将转储文件加载到调试器中，然后使用 [**. dump (创建转储文件) **](-dump--create-dump-file-.md) 命令，以小型转储格式保存新转储文件。

**注意**   尽管名称相同，但最大的 "小型转储" 文件实际上包含了比完整用户模式转储更多的信息。 例如， **dump/mf** 或 **/ma** 将创建比 **dump/f**更大、更完整的文件。

在用户模式下，**转储/m \[ **<em>MiniOptions</em> **\]** 是最佳选择。 用此开关创建的转储文件的大小可能会很小到非常大。 通过指定正确的 *MiniOptions* ，你可以精确控制所包含的信息。

## <a name="span-idminidumpsspanspan-idminidumpsspanminidumps"></a><span id="minidumps"></span><span id="MINIDUMPS"></span>小型转储

仅包含与进程关联的内存的选定部分的用户模式转储文件称为 *小型*转储。

小型转储文件的大小和内容因正在转储的程序和执行转储的应用程序而异。 通常，小型转储文件相当大，并且包括完整的内存和句柄表。 其他情况下，它会小得多，例如，它可能只包含单个线程的相关信息，或者只包含有关堆栈中实际引用的模块的信息。

名称 "小型转储" 会产生误导性，因为最大的小型转储文件实际包含的信息比 "完全" 用户模式转储多。 例如， **dump/mf** 或 **/ma** 将创建比 **dump/f**更大、更完整的文件。 出于此原因， **.dump /m**为 \[ *MiniOptions* \] 所有用户模式转储文件 **.dump /f**创建建议使用转储/m MiniOptions。

如果要使用调试器创建小型转储文件，则可以准确选择要包括的信息。 简单的 " **转储"/m** 命令将包含有关构成目标进程、线程信息和堆栈信息的已加载模块的基本信息。 这可以使用以下任一选项进行修改：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">dump 选项</th>
<th align="left">对转储文件的影响</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ma</strong></p></td>
<td align="left"><p>创建包含所有可选添加项的小型转储。 <strong>/Ma</strong>选项等效于<strong>/mfFhut</strong> --它将完整内存数据、处理数据、卸载的模块信息、基本内存信息和线程时间信息添加到小型转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mf</strong></p></td>
<td align="left"><p>将完整内存数据添加到小型转储。 将包括目标应用程序拥有的所有可访问的已提交页面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mF</strong></p></td>
<td align="left"><p>将所有基本内存信息添加到小型转储。 这会将流添加到小型转储，其中包含所有基本内存信息，而不仅仅是有关有效内存的信息。 这使调试器能够在调试小型转储时重新构造进程的完整虚拟内存布局。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mh</strong></p></td>
<td align="left"><p>将有关与目标应用程序关联的句柄的数据添加到小型转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mu</strong></p></td>
<td align="left"><p>将卸载的模块信息添加到小型转储。 此功能仅在 Windows Server 2003 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mt</strong></p></td>
<td align="left"><p>向小型转储添加其他线程信息。 这包括线程时间，在调试小型转储时，可以使用 <strong><a href="-ttime--display-thread-times-.md" data-raw-source="[.ttime (Display Thread Times)](-ttime--display-thread-times-.md)"> (ttime 显示线程时间) </a></strong> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mi</strong></p></td>
<td align="left"><p>将 <em>辅助内存</em> 添加到小型转储。 "辅助内存" 是指堆栈或后备存储中的指针所引用的任何内存以及此地址周围的小区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mp</strong></p></td>
<td align="left"><p>添加进程环境块 (PEB) 和线程环境块 (TEB) 数据添加到小型转储。 如果需要访问有关应用程序进程和线程的 Windows 系统信息，这会很有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mw</strong></p></td>
<td align="left"><p>将所有提交的读写专用页面添加到小型转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p>/md</p></td>
<td align="left"><p>将可执行映像内的所有读写数据段添加到小型转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mc</strong></p></td>
<td align="left"><p>在图像中添加代码段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mr</strong></p></td>
<td align="left"><p>从小型转储中删除堆栈的部分，并存储用于重新创建堆栈跟踪的内存。 还会删除本地变量和其他数据类型值。 此选项不会使小型转储 (小型，因为这些内存部分只是归零) ，但如果你想要保护其他应用程序的隐私，则此选项很有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mR</strong></p></td>
<td align="left"><p>从小型转储中删除完整的模块路径。 只包含模块 <em>名称</em> 。 如果要保护用户的目录结构的隐私，这是一个非常有用的选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mk "</strong> <em>FileName</em> <strong>"</strong></p></td>
<td align="left"><p> (Windows Vista 仅) 除了创建用户模式小型转储外，还会创建一个内核模式小型转储。 内核模式小型转储将限制为存储在用户模式小型转储中的相同线程。 <em>文件名</em> 必须用引号引起来。</p></td>
</tr>
</tbody>
</table>

这些选项可以组合在一起。 例如， **/mfiu** 可用于创建相当大的小型转储，或命令 **。转储/mrR** 可用于创建保留用户隐私的小型转储。 有关完整的语法详细信息，请参阅 [**。 dump (创建转储文件) **](-dump--create-dump-file-.md)。

## <a name="span-idcreatingspanspan-idcreatingspancreating-a-user-mode-dump-file"></a><span id="creating"></span><span id="CREATING"></span>创建用户模式转储文件

有多种不同的工具可用于创建用户模式转储文件： CDB、WinDbg 和 Procdump。

## <a name="span-idprocdumpspanspan-idprocdumpspanprocdump"></a><span id="procdump"></span><span id="Procdump"></span>ProcDump

ProcDump 是一个命令行实用程序，其主要用途是监视应用程序的 CPU 峰值，并在高峰期间生成故障转储，管理员或开发人员可以使用这些功能来确定高峰的原因。 ProcDump 还包括挂起的窗口监视 (使用 Windows 和任务管理器使用) 、未经处理的异常监视的相同定义，并可基于系统性能计数器的值生成转储。 它还可以用作可嵌入到其他脚本中的常规进程转储实用工具。

有关使用 Sysinternals ProcDump 实用工具创建用户模式转储文件的信息，请参阅 [ProcDump](/sysinternals/downloads/procdump)。

## <a name="span-idcdb-windbgspanspan-idcdb-windbgspancdb-and-windbg"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>CDB 和 WinDbg

CDB 和 WinDbg 可以通过多种方式创建用户模式转储文件。

### <a name="span-idcreating_a_dump_file_automaticallyspanspan-idcreating_a_dump_file_automaticallyspancreating-a-dump-file-automatically"></a><span id="creating_a_dump_file_automatically"></span><span id="CREATING_A_DUMP_FILE_AUTOMATICALLY"></span>自动创建转储文件

出现应用程序错误时，Windows 可以通过几种不同的方式进行响应，具体取决于事后调试设置。 如果这些设置指示调试工具创建转储文件，则将创建一个用户模式内存转储文件。 有关详细信息，请参阅 [启用事后调试](enabling-postmortem-debugging.md)。

### <a name="span-idcreating_dump_files_while_debuggingspanspan-idcreating_dump_files_while_debuggingspancreating-dump-files-while-debugging"></a><span id="creating_dump_files_while_debugging"></span><span id="CREATING_DUMP_FILES_WHILE_DEBUGGING"></span>在调试时创建转储文件

当 CDB 或 WinDbg 正在调试用户模式应用程序时，还可以使用 [**dump (创建转储文件) **](-dump--create-dump-file-.md) 命令创建转储文件。

此命令不会导致目标应用程序终止。 通过选择适当的命令选项，你可以创建包含所需信息的完全相同的小型转储文件。

### <a name="span-idshrinking_an_existing_dump_filespanspan-idshrinking_an_existing_dump_filespanshrinking-an-existing-dump-file"></a><span id="shrinking_an_existing_dump_file"></span><span id="SHRINKING_AN_EXISTING_DUMP_FILE"></span>收缩现有转储文件

CDB 和 WinDbg 还可用于 *收缩* 转储文件。 为此，请开始调试现有转储文件，然后使用 **dump** 命令创建大小较小的转储文件。

## <a name="span-idcdb-windbgspanspan-idcdb-windbgspan-time-travel-debugging-ttd"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span> 行程调试 (TTD) 

除了 CDB、WinDbg 和 Procdump 以外，调试用户模式应用程序的另一个选项是 (TTD) 的时间行程调试。 时间行程调试是一种工具，可让你记录正在运行的进程的执行，然后在以后向前和向后重播。 使用行程调试 (TTD) 可以通过使你 "后退" 调试器会话来更轻松地调试问题，而无需在发现 bug 之前重现问题。

TTD 可让你返回时间，以便更好地了解导致错误的条件并多次重播，以了解如何最好地解决问题。

与故障转储文件相比，TTD 具有更多优点，这通常会导致最终失败导致的代码执行。

有关 (TTD) 的时间段的详细信息，请参阅 [行程调试-概述](time-travel-debugging-overview.md)。