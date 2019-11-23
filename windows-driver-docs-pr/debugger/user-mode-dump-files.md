---
title: 用户模式转储文件
description: 用户模式转储文件
ms.assetid: bef29d75-6620-4219-b402-36fbddc4fe1f
keywords:
- 转储文件，用户模式
ms.date: 10/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 58f97674802693100fd426d77e06420e3a6c66d0
ms.sourcegitcommit: bff7fdcac628f8b62bd9df2658ca56301d1f8b07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72030802"
---
# <a name="user-mode-dump-files"></a>用户模式转储文件

本部分包括：

- [各种用户模式转储文件](#varieties)

- [创建用户模式转储文件](#creating)

有关分析转储文件的信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)。


## <a name="span-idvarietiesspanspan-idvarietiesspan-varieties-of-user-mode-dump-files"></a><span id="varieties"></span><span id="VARIETIES"></span>各种用户模式转储文件

用户模式故障转储文件有多种，但分为两类：

[完全用户模式转储](#full)

[小型转储](#minidumps)

这些转储文件之间的差异是大小之一。 小型转储通常更紧凑，可轻松发送到分析师。

**请注意**，可以通过分析转储文件来获取   多的信息。 但是，任何转储文件都不能提供与实际使用调试器直接调试故障一样多的信息。


## <a name="span-idfullspanspan-idfullspanfull-user-mode-dumps"></a><span id="full"></span><span id="FULL"></span>完全用户模式转储

完整的用户*模式转储*是基本用户模式转储文件。

此转储文件包括进程的整个内存空间、程序的可执行文件映像本身、句柄表以及在重新构建转储时使用的内存时对调试器有用的其他信息。

可以将完整的用户模式转储文件 "收缩" 到小型转储。 只需将转储文件加载到调试器中，然后使用 "[**转储" （创建转储文件）** ](-dump--create-dump-file-.md)命令以小型转储格式保存新转储文件。

  **请注意**，尽管名称相同，但最大的 "小型转储" 文件实际上包含了比完整用户模式转储更多的信息。 例如， **dump/mf**或 **/ma**将创建比**dump/f**更大、更完整的文件。


在用户模式下， **\[** <em>MiniOptions</em> **\]** 是最佳选择。 用此开关创建的转储文件的大小可能会很小到非常大。 通过指定正确的*MiniOptions* ，你可以精确控制所包含的信息。



## <a name="span-idminidumpsspanspan-idminidumpsspanminidumps"></a><span id="minidumps"></span><span id="MINIDUMPS"></span>小型转储

仅包含与进程关联的内存的选定部分的用户模式转储文件称为*小型*转储。

小型转储文件的大小和内容因正在转储的程序和执行转储的应用程序而异。 通常，小型转储文件相当大，并且包括完整的内存和句柄表。 其他情况下，它会小得多，例如，它可能只包含单个线程的相关信息，或者只包含有关堆栈中实际引用的模块的信息。

名称 "小型转储" 会产生误导性，因为最大的小型转储文件实际包含的信息比 "完全" 用户模式转储多。 例如， **dump/mf**或 **/ma**将创建比**dump/f**更大、更完整的文件。 出于此原因，为所有用户模式转储文件创建，请使用**转储/m**\[*MiniOptions*\] **。**

如果要使用调试器创建小型转储文件，则可以准确选择要包括的信息。 简单的 "**转储"/m**命令将包含有关构成目标进程、线程信息和堆栈信息的已加载模块的基本信息。 这可以使用以下任一选项进行修改：

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
<td align="left"><p>向小型转储添加其他线程信息。 这包括线程时间，在调试小型转储时，可以使用<strong><a href="-ttime--display-thread-times-.md" data-raw-source="[.ttime (Display Thread Times)](-ttime--display-thread-times-.md)">ttime （显示线程时间）</a></strong>来显示线程时间。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mi</strong></p></td>
<td align="left"><p>将<em>辅助内存</em>添加到小型转储。 "辅助内存" 是指堆栈或后备存储中的指针所引用的任何内存以及此地址周围的小区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mp</strong></p></td>
<td align="left"><p>将进程环境块（PEB）和线程环境块（TEB）数据添加到小型转储。 如果需要访问有关应用程序进程和线程的 Windows 系统信息，这会很有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mw</strong></p></td>
<td align="left"><p>将所有提交的读写专用页面添加到小型转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/md</strong></p></td>
<td align="left"><p>将可执行映像内的所有读写数据段添加到小型转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mc</strong></p></td>
<td align="left"><p>在图像中添加代码段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mr</strong></p></td>
<td align="left"><p>从小型转储中删除堆栈的部分，并存储用于重新创建堆栈跟踪的内存。 还会删除本地变量和其他数据类型值。 此选项不会使小型转储更小（因为这些内存部分只是归零），但如果你想要保护其他应用程序的隐私，则此选项很有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mR</strong></p></td>
<td align="left"><p>从小型转储中删除完整的模块路径。 只包含模块<em>名称</em>。 如果要保护用户的目录结构的隐私，这是一个非常有用的选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mk "</strong> <em>FileName</em> <strong>"</strong></p></td>
<td align="left"><p>（仅适用于 Windows Vista）除了用户模式小型转储，还会创建一个内核模式小型转储。 内核模式小型转储将限制为存储在用户模式小型转储中的相同线程。 <em>文件名</em>必须用引号引起来。</p></td>
</tr>
</tbody>
</table>


这些选项可以组合在一起。 例如， **/mfiu**可用于创建相当大的小型转储，或命令 **。转储/mrR**可用于创建保留用户隐私的小型转储。 有关完整的语法详细信息，请参阅[**dump （创建转储文件）** ](-dump--create-dump-file-.md)。


## <a name="span-idcreatingspanspan-idcreatingspancreating-a-user-mode-dump-file"></a><span id="creating"></span><span id="CREATING"></span>创建用户模式转储文件

有多种不同的工具可用于创建用户模式转储文件： CDB、WinDbg、Windows 错误报告（WER）、UserDump 和 ADPlus。

有关通过 ADPlus 创建用户模式转储文件的信息，请参阅[adplus](adplus.md)。

有关通过 WER 创建用户模式转储文件的信息，请参阅[Windows 错误报告](windows-error-reporting.md)。


## <a name="span-idddk_choosing_the_best_tool_dbgspanspan-idddk_choosing_the_best_tool_dbgspanchoosing-the-best-tool"></a><span id="ddk_choosing_the_best_tool_dbg"></span><span id="DDK_CHOOSING_THE_BEST_TOOL_DBG"></span>选择最佳工具

可以通过几种不同的工具来创建用户模式转储文件。 在大多数情况下，ADPlus 是使用的最佳工具。

下表显示了每个工具的功能。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">功能</th>
<th align="left"><a href="adplus.md" data-raw-source="[ADPlus](adplus.md)">ADPlus</a></th>
<th align="left"><a href="windows-error-reporting.md" data-raw-source="[Windows Error Reporting](windows-error-reporting.md)">Windows 错误报告</a></th>
<th align="left"><a href="#cdb-windbg" data-raw-source="[CDB and WinDbg](#cdb-windbg)">CDB 和 WinDbg</a></th>
<th align="left"><a href="#userdump" data-raw-source="[UserDump](#userdump)">UserDump</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在应用程序崩溃时创建转储文件（事后调试）</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>在应用程序 "挂起" 时创建转储文件（停止响应但实际上不会崩溃）</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在应用程序遇到异常时创建转储文件</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>在应用程序正常运行时创建转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>从在启动过程中失败的应用程序创建转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>收缩现有转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 
## <a name="span-idcdb-windbgspanspan-idcdb-windbgspancdb-and-windbg"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>CDB 和 WinDbg


CDB 和 WinDbg 可以通过多种方式创建用户模式转储文件。

### <a name="span-idcreating_a_dump_file_automaticallyspanspan-idcreating_a_dump_file_automaticallyspancreating-a-dump-file-automatically"></a><span id="creating_a_dump_file_automatically"></span><span id="CREATING_A_DUMP_FILE_AUTOMATICALLY"></span>自动创建转储文件

出现应用程序错误时，Windows 可以通过几种不同的方式进行响应，具体取决于事后调试设置。 如果这些设置指示调试工具创建转储文件，则将创建一个用户模式内存转储文件。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

### <a name="span-idcreating_dump_files_while_debuggingspanspan-idcreating_dump_files_while_debuggingspancreating-dump-files-while-debugging"></a><span id="creating_dump_files_while_debugging"></span><span id="CREATING_DUMP_FILES_WHILE_DEBUGGING"></span>在调试时创建转储文件

当 CDB 或 WinDbg 正在调试用户模式应用程序时，您还可以使用[**dump （创建转储文件）** ](-dump--create-dump-file-.md)命令创建转储文件。

此命令不会导致目标应用程序终止。 通过选择适当的命令选项，你可以创建包含所需信息的完全相同的小型转储文件。

### <a name="span-idshrinking_an_existing_dump_filespanspan-idshrinking_an_existing_dump_filespanshrinking-an-existing-dump-file"></a><span id="shrinking_an_existing_dump_file"></span><span id="SHRINKING_AN_EXISTING_DUMP_FILE"></span>收缩现有转储文件

CDB 和 WinDbg 还可用于*收缩*转储文件。 为此，请开始调试现有转储文件，然后使用**dump**命令创建大小较小的转储文件。


## <a name="span-iduserdumpspanspan-iduserdumpspanuserdump"></a><span id="userdump"></span><span id="USERDUMP"></span>UserDump

UserDump 工具（Userdump）（也称为用户模式进程转储）可以创建用户模式转储文件。

UserDump 及其文档是 OEM 支持工具包的一部分。

有关详细信息和下载这些工具，请参阅[如何使用 Userdump 工具创建转储文件](https://go.microsoft.com/fwlink/p/?LinkId=241339)并按照该页上的说明进行操作。 此外，当 CDB 或 WinDbg 正在调试用户模式应用程序时，还可以使用[dump （创建转储文件）命令](-dump--create-dump-file-.md)创建转储文件。




 





