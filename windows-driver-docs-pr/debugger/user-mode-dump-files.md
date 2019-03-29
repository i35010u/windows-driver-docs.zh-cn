---
title: 用户模式转储文件
description: 用户模式转储文件
ms.assetid: bef29d75-6620-4219-b402-36fbddc4fe1f
keywords:
- 转储文件、 用户模式
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8c5e96f53806931cfc846ef7167e204a23dc6d12
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464193"
---
# <a name="user-mode-dump-files"></a>用户模式转储文件

本部分包括：

- [类型的用户模式转储文件](#varieties)

- [正在创建用户模式转储文件](#creating)

有关分析转储文件的信息，请参阅[分析用户模式转储文件](analyzing-a-user-mode-dump-file.md)。


## <a name="span-idvarietiesspanspan-idvarietiesspan-varieties-of-user-mode-dump-files"></a><span id="varieties"></span><span id="VARIETIES"></span> 类型的用户模式转储文件

有几种用户模式故障转储文件，但它们被分为两个类别：

[完整的用户模式转储](#full)

[小型转储](#minidumps)

这些转储文件之间的差异是大小之一。 小型转储是通常更紧凑，并可以轻松地发送给分析师。

**请注意**  多的信息可以通过分析转储文件。 但是，没有转储文件可以提供尽可能多的信息实际上直接使用调试器调试在发生崩溃。


## <a name="span-idfullspanspan-idfullspanfull-user-mode-dumps"></a><span id="full"></span><span id="FULL"></span>完整的用户模式转储

一个*完整的用户模式转储*是基本的用户模式转储文件。

此转储文件包含进程、 程序的可执行映像本身、 句柄表中和对调试程序将非常有用的其他信息的整个内存空间。

就可以完全用户模式转储文件"收缩"到小型转储。 只需加载到调试器的转储文件，然后使用[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)命令以小型转储格式保存新的转储文件。

**请注意**  尽管其名称，最大的"小型转储"文件实际包含比完全用户模式转储的详细信息。 例如， **.dump /mf**或 **.dump /ma**将创建更大、 更完整的文件，而非 **.dump /f**。


在用户模式下 **.dump /m\[**<em>MiniOptions</em> **\]** 是最佳选择。 使用此开关创建的转储文件中从很小到非常大的大小而异。 通过指定了正确*MiniOptions*可以控制哪些信息究竟是包含。



## <a name="span-idminidumpsspanspan-idminidumpsspanminidumps"></a><span id="minidumps"></span><span id="MINIDUMPS"></span>小型转储

调用用户模式转储文件，包括仅所选的部分关联的进程的内存*小型转储*。

大小和小型转储文件的内容取决于要转储的程序和应用程序执行的转储。 有时，一个小型转储文件非常大，包括完整的内存和句柄表。 其他情况下，它是要小得多，例如，它可能仅包含有关单个线程的信息，或仅包含实际引用在堆栈中的模块的相关信息。

名称为"小型转储"是具有误导性，因为最大的小型转储文件实际包含比"完整"的用户模式转储的详细信息。 例如， **.dump /mf**或 **.dump /ma**将创建更大、 更完整的文件，而非 **.dump /f**。 出于此原因， **.dump /m**\[*MiniOptions* \]建议 **.dump /f**为所有用户模式转储文件的创建过程。

如果要使用调试器创建一个小型转储文件，可以选择完全要提供的信息。 一个简单 **.dump /m**命令将包括有关使目标进程中，多线程的信息，以及堆栈信息已加载模块的基本信息。 可使用任何以下选项对此进行了修改：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">.dump 选项</th>
<th align="left">转储文件无效</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/ma</strong></p></td>
<td align="left"><p>与所有可选的新增内容创建一个小型转储。 <strong>/Ma</strong>选项等同于<strong>/mfFhut</strong> -它将完整的内存数据、 处理的数据、 卸载的模块信息、 基本内存信息和线程时间信息添加到小型转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mf</strong></p></td>
<td align="left"><p>将完整的内存数据添加到小型转储。 将包含在目标应用程序所拥有的所有可访问已提交的页面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mF</strong></p></td>
<td align="left"><p>将所有基本内存信息添加到小型转储。 这将流添加到包含所有基本内存信息，而不仅仅是有效的内存信息的小型转储。 这使调试器能够在调试小型转储时重新构造完整的虚拟内存布局的过程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mh</strong></p></td>
<td align="left"><p>添加有关小型转储到目标应用程序与关联的句柄的数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mu</strong></p></td>
<td align="left"><p>将卸载的模块信息添加到小型转储。 这是仅在 Windows Server 2003 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mt</strong></p></td>
<td align="left"><p>将其他线程信息添加到小型转储。 这包括线程时间，可以使用显示<strong><a href="-ttime--display-thread-times-.md" data-raw-source="[.ttime (Display Thread Times)](-ttime--display-thread-times-.md)">.ttime （显示线程时间）</a></strong>调试小型转储时。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mi</strong></p></td>
<td align="left"><p>将添加<em>辅助内存</em>到小型转储。 辅助内存是堆栈或后备存储，再加上的小区域周围此地址的指针所引用的任何内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mp</strong></p></td>
<td align="left"><p>将进程环境块 (PEB) 和线程环境块 (TEB) 数据添加到小型转储。 这很有用，如果需要访问 Windows 应用程序的进程和线程的系统信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mw</strong></p></td>
<td align="left"><p>将所有已提交的读写专用页添加到小型转储。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/md</strong></p></td>
<td align="left"><p>将可执行映像中的所有读写数据段都添加到小型转储。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mc</strong></p></td>
<td align="left"><p>将添加在图像中的代码段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mr</strong></p></td>
<td align="left"><p>从小型转储中删除不是可用于重新创建的堆栈跟踪这些部分的堆栈和应用商店的内存。 本地变量和其他数据类型值也将被删除。 此选项不会进行小型转储较小 （自这些内存部分只是归零），但如果你想要保护隐私的其他应用程序非常有用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/mR</strong></p></td>
<td align="left"><p>从小型转储中删除所有模块路径。 仅模块<em>名称</em>会包含。 如果你想要保护隐私的用户的目录结构，这是一个有用的选项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/mk "</strong> <em>FileName</em> <strong>"</strong></p></td>
<td align="left"><p>(仅适用于 Windows Vista)创建用户模式下小型转储除了一个内核模式小型转储。 内核模式小型转储将限制为存储在用户模式下小型转储中的同一个线程。 <em>文件名</em>必须括在引号中。</p></td>
</tr>
</tbody>
</table>


可以组合这些选项。 例如，命令 **.dump /mfiu**可用于创建相当大的小型转储或该命令 **.dump /mrR**可用于创建保留用户的隐私信息的小型转储。 有关完整语法的详细信息，请参阅[ **.dump （创建转储文件）**](-dump--create-dump-file-.md)。


## <a name="span-idcreatingspanspan-idcreatingspancreating-a-user-mode-dump-file"></a><span id="creating"></span><span id="CREATING"></span>正在创建用户模式转储文件

有几个不同的工具可用于创建用户模式转储文件：CDB、 WinDbg、 Windows 错误报告 (WER)、 用户转储和 ADPlus。

有关创建通过 ADPlus 用户模式转储文件的信息，请参阅[ADPlus](adplus.md)。

有关创建通过 WER 的用户模式转储文件的信息，请参阅[Windows 错误报告](windows-error-reporting.md)。


## <a name="span-idddkchoosingthebesttooldbgspanspan-idddkchoosingthebesttooldbgspanchoosing-the-best-tool"></a><span id="ddk_choosing_the_best_tool_dbg"></span><span id="DDK_CHOOSING_THE_BEST_TOOL_DBG"></span>选择最佳工具

有几种不同的工具，可以创建用户模式转储文件。 在大多数情况下，ADPlus 是要使用的最佳工具。

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
<td align="left"><p>应用程序崩溃 （事后调试） 时创建转储文件</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>创建转储文件时的应用程序"挂起"（停止响应但不会实际崩溃）</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>应用程序遇到的异常时创建转储文件</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>通常情况下运行应用程序时创建转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p>从在启动过程失败的应用程序创建转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p>收缩现有的转储文件</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 
## <a name="span-idcdb-windbgspanspan-idcdb-windbgspancdb-and-windbg"></a><span id="cdb-windbg"></span><span id="CDB-WINDBG"></span>CDB 和 WinDbg


CDB 和 WinDbg 可以创建用户模式转储文件中有许多种。

### <a name="span-idcreatingadumpfileautomaticallyspanspan-idcreatingadumpfileautomaticallyspancreating-a-dump-file-automatically"></a><span id="creating_a_dump_file_automatically"></span><span id="CREATING_A_DUMP_FILE_AUTOMATICALLY"></span>自动创建一个转储文件

当应用程序出错时，Windows 可以以多种不同方式，具体取决于调试设置总结响应。 如果这些设置指明调试工具创建转储文件，将创建一个用户模式内存转储文件。 有关详细信息，请参阅[启用事后调试](enabling-postmortem-debugging.md)。

### <a name="span-idcreatingdumpfileswhiledebuggingspanspan-idcreatingdumpfileswhiledebuggingspancreating-dump-files-while-debugging"></a><span id="creating_dump_files_while_debugging"></span><span id="CREATING_DUMP_FILES_WHILE_DEBUGGING"></span>调试时创建转储文件

CDB 或 WinDbg 是在调试时在用户模式应用程序，还可以[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)命令以创建转储文件。

此命令不会导致目标应用程序终止。 通过选择适当的命令选项，可以创建一个包含完全想的信息量的小型转储文件。

### <a name="span-idshrinkinganexistingdumpfilespanspan-idshrinkinganexistingdumpfilespanshrinking-an-existing-dump-file"></a><span id="shrinking_an_existing_dump_file"></span><span id="SHRINKING_AN_EXISTING_DUMP_FILE"></span>收缩现有的转储文件

CDB 和 WinDbg 还可用于*收缩*转储文件。 若要执行此操作，开始调试一个现有的转储文件，以及如何将 **.dump**命令来创建较小的转储文件。


## <a name="span-iduserdumpspanspan-iduserdumpspanuserdump"></a><span id="userdump"></span><span id="USERDUMP"></span>UserDump

用户转储工具 (Userdump.exe)，也称为用户模式进程转储，可以创建用户模式转储文件。

用户转储和及其说明文档是 OEM 支持工具程序包的一部分。

有关详细信息并下载这些工具，请参阅[如何使用 Userdump.exe 工具创建转储文件](https://go.microsoft.com/fwlink/p/?LinkId=241339)并按照该页上的说明。 此外，当 CDB 或 WinDbg 调试在用户模式应用程序，还可以使用[.dump （创建转储文件） 命令](-dump--create-dump-file-.md)创建转储文件。




 





