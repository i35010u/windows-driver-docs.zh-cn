---
title: GFlags 命令
description: 若要使用 GFlags，请在命令行中键入以下命令。 可以使用 GFlags 命令和 "全局标志" 对话框。
ms.assetid: 832b7269-623a-4f32-8bda-1059087bab09
keywords:
- GFlags 命令 Windows 调试
ms.date: 06/12/2018
topic_type:
- apiref
api_name:
- GFlags Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 682941016410914efb283144a5071d4489790718
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284899"
---
# <a name="gflags-command-overview"></a>GFlags 命令概述

有关如何安装和查找 gflags 的常规信息，请参阅[gflags](gflags.md)。

可以使用 GFlags 命令和 "[全局标志" 对话框](global-flags-dialog-box.md)。

## <a name="gflags-command-usage"></a>GFlags 命令用法 

若要使用 GFlags，请在命令行中键入以下命令。


打开 "GFlags" 对话框：

```console
gflags
```

若要设置或清除注册表中的全局标志：

```console
gflags /r [{+ | -}Flag [{+ | -}Flag...]]
```

设置或清除当前会话的全局标志：

```console
gflags /k [{+ | -}Flag [{+ | -}Flag...]]
```

设置或清除映像文件的全局标志：

```console
gflags /i ImageFile [{+ | -}Flag [{+ | -}Flag...]]
gflags /i ImageFile /tracedb SizeInMB
```

设置或清除 "特殊池" 功能（Windows Vista 和更高版本）

```console
gflags {/r | /k} {+ | -}spp {PoolTag | 0xSize}
```

启用或禁用对象引用跟踪功能（Windows Vista 和更高版本）

```console
gflags {/ro | /ko} [/p] [/i ImageFile | /t PoolTag;[PoolTag...]]
```

```console
gflags {/ro | /ko} /d
```

启用和配置页堆验证：

```console
gflags /p /enable ImageFile  [ /full [/backwards] | /random Probability | /size SizeStart SizeEnd | /address AddressStart AddressEnd | /dlls DLL [DLL...] ] 
[/debug ["DebuggerCommand"] | /kdebug] [/unaligned] [/notraces] [/fault Rate [TimeOut]] [/leaks] [/protect] [/no_sync] [/no_lock_checks] 
```

禁用页堆验证：

```console
gflags /p [/disable ImageFile] [/?]
```

显示帮助：

```console
glags /?
```

## <a name="span-idddk_gflags_commands_dtoolsspanspan-idddk_gflags_commands_dtoolsspanparameters"></a><span id="ddk_gflags_commands_dtools"></span><span id="DDK_GFLAGS_COMMANDS_DTOOLS"></span>Parameters


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span>*标志*   
指定三字母缩写（*FlagAbbr*）或十六进制值（*FlagHex*），表示调试功能。 缩写和十六进制值在[GFlags 标志表](gflags-flag-table.md)中列出。

使用下列标志格式之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">格式</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-</strong>{<strong>+</strong> | }<em>FlagAbbr</em></p></td>
<td align="left"><p>设置（+）或清除（-）标志缩写所表示的标志。 如果没有加号（+）或减号（-）符号，则该命令不起作用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-</strong>[<strong>+</strong> | ]<em>FlagHex</em></p></td>
<td align="left"><p>添加（+）或减去（-）标志的十六进制值。 在 sum 中包含标志时，将设置该标志。 Add （+）是默认值。 输入表示单个标志的十六进制值（不含0x），或输入多个标志的十六进制值的总和。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageFile______"></span><span id="_______imagefile______"></span><span id="_______IMAGEFILE______"></span>*ImageFile*   
指定可执行文件的名称，包括文件扩展名（例如，notepad.exe 或 mydll）。

<span id="________r______"></span><span id="________R______"></span> **/r**   
Registry. 显示或更改注册表中存储的系统范围内调试标志。 这些设置在重新启动 Windows 时生效并保持有效，直到你更改它们为止。

如果没有其他参数， **gflags/r**将显示注册表中设置的系统范围内的标志。

<span id="________k______"></span><span id="________K______"></span> **/k**   
内核标志设置。 显示或更改此会话的系统范围内调试标志。 这些设置将立即生效，但在 Windows 关闭时将丢失。 这些设置会影响在此命令完成后启动的进程。

如果没有其他参数， **gflags/k**将显示为当前会话设置的系统范围标志。

<span id="________i______"></span><span id="________I______"></span> **/i**   
图像文件设置。 显示或更改特定进程的调试标志。 这些设置存储在注册表中。 它们对于此进程的所有新实例都是有效的，它们始终有效，直到你更改它们。

如果没有其他参数， **gflags/I** *ImageFile*将显示为指定进程设置的标志。

<span id="________tracedb_______SizeInMB______"></span><span id="________tracedb_______sizeinmb______"></span><span id="________TRACEDB_______SIZEINMB______"></span> **/tracedb***SizeInMB*   
设置进程的用户模式堆栈跟踪数据库的最大大小。 若要使用此参数，必须为进程设置[创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md)（ust）标志。

*SizeInMB*是一个整数，表示十进制单位的兆字节数。 默认值为最小大小（8 MB）;没有最大大小。 若要恢复为默认大小，请将*SizeInMB*设置为0。

<span id="_______spp______"></span><span id="_______SPP______"></span>**spp**   
（Windows Vista 和更高版本。）设置或清除[特殊池](special-pool.md)功能。 有关示例，请参阅[示例14：配置特殊池](example-14---configuring-special-pool.md)。

<span id="_______PoolTag______"></span><span id="_______pooltag______"></span><span id="_______POOLTAG______"></span>*PoolTag*   
（Windows Vista 和更高版本。）指定 "[特殊池](special-pool.md)" 功能的池标记。 仅与**spp**标志一起使用。

为*PoolTag*输入四字符模式，如 Tag1。 它可以包含 **？** （替换为任意单个字符）和 **\*** （替换为多个字符）通配符。 例如，Fat\*或 Av？4。 池标记始终区分大小写。

<span id="0xSize______"></span><span id="0xsize______"></span><span id="0XSIZE______"></span>**0x * * * 大小*   
（Windows Vista 和更高版本。）指定特殊池功能的大小范围。 仅与**spp**标志一起使用。 有关选择大小值的指南，请参阅[特殊池中](special-pool.md)的 "选择分配大小"。

<span id="________ro______"></span><span id="________RO______"></span> **/ro**   
启用、禁用和显示注册表中的[对象引用跟踪](object-reference-tracing.md)设置。 若要使此设置生效，必须重新启动 Windows。

如果没有其他参数， **/ro**将在注册表中显示对象引用跟踪设置。

若要启用对象引用跟踪，则必须在命令中至少包含一个池标记（ **/T** *PoolTag*）或一个映像文件（ **/i** ImageFile）。 有关详细信息， [请参阅示例15：使用对象引用跟踪](example-15--using-object-reference-tracing.md)。

下表列出了与 **/ro**有效的子参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/t</strong><em>PoolTags</em></p></td>
<td align="left"><p>将跟踪限制为具有指定的池标记的对象。 使用分号（<strong>;</strong>）分隔标记名。 输入最多16个池标记。</p>
<p>为<em>PoolTags</em>输入四字符模式，如 Tag1。</p>
<p>如果指定多个池标记，Windows 将跟踪具有指定的任何池标记的对象。</p>
<p>如果未指定任何池标记，Windows 将跟踪该映像创建的所有对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong><em>ImageFile</em></p></td>
<td align="left"><p>将跟踪限制为由具有指定图像文件的进程创建的对象。 只能指定一个带有<strong>/i</strong>参数的映像文件。</p>
<p>输入图像文件名，如 notepad.exe，最多64个字符。 "系统" 和 "空闲" 不是有效的映像名称。</p>
<p>如果未指定图像文件，则 Windows 将跟踪具有指定池标记的所有对象。 如果同时指定了图像文件（<strong>/i</strong>）和一个或多个池标记（<strong>/T</strong>），Windows 将跟踪对象，这些对象具有指定的映像创建的任何指定的池标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/d</strong></p></td>
<td align="left"><p>清除对象引用跟踪功能设置。 与<strong>/ro</strong>一起使用时，它会清除注册表中的设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>撤消. 跟踪数据将保留，直到禁用对象引用跟踪或关闭或重新启动计算机。 默认情况下，销毁对象时，对象的跟踪数据将被丢弃。</p></td>
</tr>
</tbody>
</table>

 

<span id="________ko______"></span><span id="________KO______"></span> **/ko**   
启用、禁用和显示内核标志（运行时）[对象引用跟踪](object-reference-tracing.md)设置。 对此设置的更改将立即生效，但会在系统关闭或重新启动时丢失。 有关详细信息， [请参阅示例15：使用对象引用跟踪](example-15--using-object-reference-tracing.md)。

如果没有其他参数， **/ko**会显示内核标志（运行时）对象引用跟踪设置。

若要启用对象引用跟踪，则必须在命令中至少包含一个池标记（ **/T** *PoolTag*）或一个映像文件（ **/i** *ImageFile*）。

下表列出了与 **/ko**有效的子参数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/t</strong><em>PoolTags</em></p></td>
<td align="left"><p>将跟踪限制为具有指定的池标记的对象。 使用分号（<strong>;</strong>）分隔标记名。 输入最多16个池标记。</p>
<p>为<em>PoolTags</em>输入四字符模式，如 Tag1。</p>
<p>如果指定多个池标记，Windows 将跟踪具有指定的任何池标记的对象。</p>
<p>如果未指定任何池标记，Windows 将跟踪该映像创建的所有对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong><em>ImageFile</em></p></td>
<td align="left"><p>将跟踪限制为由具有指定图像文件的进程创建的对象。 只能指定一个带有<strong>/i</strong>参数的映像文件。</p>
<p>如果未指定图像文件，则 Windows 将跟踪具有指定池标记的所有对象。</p>
<p>如果同时指定了图像文件（<strong>/i</strong>）和一个或多个池标记（<strong>/T</strong>），Windows 将跟踪对象，这些对象具有指定的映像创建的任何指定的池标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/d</strong></p></td>
<td align="left"><p>清除对象引用跟踪功能设置。 与<strong>/ro</strong>一起使用时，它会清除注册表中的设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>撤消. 跟踪数据将保留，直到禁用对象引用跟踪或关闭或重新启动计算机。 默认情况下，销毁对象时，对象的跟踪数据将被丢弃。</p></td>
</tr>
</tbody>
</table>

 

<span id="________p______"></span><span id="________P______"></span> **/p**   
为进程设置页堆验证选项。

如果没有其他参数， **gflags/p**将显示启用了页面堆验证的图像文件的列表。

页堆验证监视动态堆内存操作（包括分配操作和自由操作），并在检测到堆错误时导致调试器中断。

<span id="________disable_______ImageFile______"></span><span id="________disable_______imagefile______"></span><span id="________DISABLE_______IMAGEFILE______"></span> **/disable***ImageFile*   
为指定的映像文件关闭页堆验证（标准或完整）。

此命令等效于关闭进程的[启用页堆](enable-page-heap.md)（hpa）标志（**gflags/i** **hpa**）。 可以交换使用这些命令。

<span id="________enable_______ImageFile______"></span><span id="________enable_______imagefile______"></span><span id="________ENABLE_______IMAGEFILE______"></span> **/enable***ImageFile*   
为指定的映像文件启用页堆验证。

默认情况下， **/enable**参数将为映像文件启用*标准*页堆验证。 若要为映像文件启用*完整*的页堆验证，请将 **/full**参数添加到命令中，或将 **/i**参数与 **+ hpa**标志一起使用。

<span id="________full______"></span><span id="________FULL______"></span> **/full**   
为进程启用整页堆验证。 整页堆验证在每次分配结束时放置保留虚拟内存的区域。

使用此参数等效于打开进程的[启用页堆](enable-page-heap.md)（hpa）标志（**gflags/i** *ImageFile* **+ hpa**）。 可以交换使用这些命令。

<span id="________backwards______"></span><span id="________BACKWARDS______"></span> **/backwards**   
将保留的虚拟内存的区域放置在分配的开头，而不是放置在结尾处。 因此，调试器将捕获缓冲区开头的溢出，而不是缓冲区末尾的溢出。 仅对 **/full**参数有效。

<span id="________random_______Probability______"></span><span id="________random_______probability______"></span><span id="________RANDOM_______PROBABILITY______"></span> **/random***概率*   
根据指定的概率，为每个分配选择完整或标准页堆验证。

*概率*是0到100之间的十进制整数，用于表示整页堆验证的概率。 100的概率与使用 **/full**参数相同。 概率0与使用标准页堆验证相同。

<span id="________size________SizeStart_SizeEnd______"></span><span id="________size________sizestart_sizeend______"></span><span id="________SIZE________SIZESTART_SIZEEND______"></span> **/size***SizeStart SizeEnd*   
启用针对指定大小范围内的分配的完整页堆验证，并为该进程的所有其他分配启用标准页堆验证。

*SizeStart*和*SizeEnd*是十进制整数。 默认值是所有分配的标准页堆验证。

<span id="________address________AddressStart_AddressEnd______"></span><span id="________address________addressstart_addressend______"></span><span id="________ADDRESS________ADDRESSSTART_ADDRESSEND______"></span> **/address***AddressStart AddressEnd*   
为在运行时调用堆栈上指定地址范围内的返回地址时分配的内存启用完整页堆验证。 它为该进程的所有其他分配启用标准页堆验证。

若要使用此功能，请指定包含用可疑分配调用函数的所有函数的地址的范围。 发生可疑分配时，调用堆栈的地址将位于调用堆栈上。

*AddressStart*和*AddressEnd*指定在分配堆栈跟踪中搜索的地址范围。 以十六进制格式指定地址，如0xAABBCCDD。

在 Windows Server 2003 及更早版本的系统上， **/address**参数仅在基于*x*86 的计算机上有效。 在 Windows Vista 上：它在所有支持的体系结构上都有效。

<span id="________dlls_DLL___DLL...__"></span><span id="________dlls_dll___dll...__"></span><span id="________DLLS_DLL___DLL...__"></span> **/dlls***DLL*，DLL... \[\]   
启用针对指定 Dll 请求的分配的完整页堆验证，并为进程的所有其他分配启用标准页堆验证。

*DLL*是包含其文件扩展名的二进制文件的名称。 指定的文件必须是在执行过程中加载的函数库。

<span id="________debug______"></span><span id="________DEBUG______"></span> **/debug**   
自动启动调试器下的 **/enable**参数指定的进程。

默认情况下，此参数将使用 NTSD 调试器和命令行**ntsd-g-g-x**并启用页堆，但你可以使用*DebuggerCommand*变量指定其他调试器和命令行。

有关 NTSD 的信息，请参阅[使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

对于难以从命令提示符启动的程序以及其他进程启动的程序，此选项很有用。

<span id="_DebuggerCommand_______"></span><span id="_debuggercommand_______"></span><span id="_DEBUGGERCOMMAND_______"></span> **"** <em>DebuggerCommand</em> **"**    
指定调试器和发送到调试器的命令。 此带引号的字符串可以包括调试器的完全限定路径、调试器名称和调试器解释的命令参数。 需要引号。

如果该命令包含调试器路径，则该路径不能包含任何其他引号。 如果出现其他引号，命令外壳（*cmd.exe*）将误认为命令。

<span id="________kdebug______"></span><span id="________KDEBUG______"></span> **/kdebug**   
使用命令行**ntsd-g-g-g**，自动启动由 ntsd 参数在 ntsd 调试程序中**指定的进程**，并启用页堆，并控制将 NTSD 重定向到内核调试器。

有关 NTSD 的信息，请参阅[使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

<span id="________unaligned______"></span><span id="________UNALIGNED______"></span> **/unaligned**   
将每个分配的结束时间与页尾边界对齐，即使在这种情况下，开始地址未在8字节块上对齐。 默认情况下，堆管理器保证分配的起始地址在8字节块上对齐。

此选项用于检测不逐字节的错误。 如果将此参数与 **/full**参数一起使用，则保留虚拟内存的区域将在分配的最后一个字节后开始，并在进程尝试读取或写入除分配之外的一个字节时立即发生错误。

<span id="________decommit______"></span><span id="________DECOMMIT______"></span> **/decommit**   
此选项不再有效。 它被接受，但被忽略。

Windows 2000 中包含的 PageHeap program （PageHeap）通过在分配后放置不可访问的页面来实现完整的页堆验证。 在该工具中， **/decommit**参数会将保留虚拟内存的区域替换为不可访问的页面。 在此版本的 GFlags 中，始终使用保留的虚拟内存区域来实现整页堆验证。

<span id="________notraces______"></span><span id="________NOTRACES______"></span> **/notraces**   
指定不保存运行时堆栈跟踪。

此选项会略微提高性能，但会使调试变得更加困难。 此参数有效，但不建议使用它。

<span id="________fault______"></span><span id="________FAULT______"></span> **/fault**   
强制程序的内存分配按指定的速率失败，并在指定的超时时间之后失败。

此参数将堆分配错误插入到所测试的映像文件中（一种称为 "错误注入" 的做法），这样，某些内存分配将会失败，因为在内存不足的情况下，可能会发生这种情况。 此测试可帮助检测处理分配失败时出现的错误，例如未能释放资源。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><em>分级</em></p></td>
<td align="left"><p>指定1（. 01%）中的十进制整数到10000（100%），表示分配失败的概率。 默认值为100（1%）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>TimeOut</em></p></td>
<td align="left"><p>确定程序的开始与错误注入例程的开头之间的时间间隔。</p>
<p><em>超时</em>值以秒为单位。 默认值为5（秒）。</p></td>
</tr>
</tbody>
</table>

 

<span id="________leaks______"></span><span id="________LEAKS______"></span> **/leaks**   
在进程结束时检查堆泄漏。

**/Leaks**参数禁用整页堆。 当使用 **/leaks**时，将忽略用于修改 **/full**参数的 **/full**参数和参数，如 **/backwards**，GFlags 将使用泄漏检查来执行标准页堆验证。

<span id="________protect______"></span><span id="________PROTECT______"></span> **/protect**   
保护堆内部结构。 此测试用于检测随机堆损坏。 这会使执行速度大大降低。

<span id="________no_sync______"></span><span id="________NO_SYNC______"></span> **/no\_同步**   
检查不同步的访问。 如果此参数检测到使用堆\_创建的堆，则不会对其他线程访问任何\_序列化标志。

不要使用此标志调试包含自定义堆管理器的程序。 同步堆访问的函数会导致页堆验证器报告不存在的同步错误。

<span id="________no_lock_checks______"></span><span id="________NO_LOCK_CHECKS______"></span> **/no\_锁定检查\_**    
禁用临界区验证程序。

<span id="_______________"></span> **/?**    
显示 GFlags 的帮助。 带有 **/p**、 **/？** 显示 GFlags 中的页堆验证选项的帮助。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

键入不带参数的**gflags**将打开 "**全局标志**" 对话框。

键入**gflags/p**而不使用其他参数将显示启用了页面堆验证的程序的列表。

若要清除所有标志，请将*标志*设置为 **-FFFFFFFF**。 （将 "*标志*" 设置为 "0" 会将零添加到当前标志值。 它不会清除所有标志。）

将映像文件的*标志*设置为**FFFFFFFF**时，Windows 将清除所有标志，并删除映像文件的注册表子项中的 GlobalFlag 条目。 子项仍保留。

页面堆 **/enable**操作的 **/full**、 **/random**、 **/size**、 **/address**和 **/dlls**参数确定哪些分配服从页堆验证和使用的验证方法。 在每个命令中只能使用这些参数中的一个。 默认为进程的所有分配的标准页堆验证。 其余参数设置页堆验证选项。

GFlags 中的页堆功能仅监视使用标准 Windows 堆管理器函数（**HeapAlloc**、 **GlobalAlloc**、 **LocalAlloc**、 **malloc**、 **new**、 **new\[ \]的堆内存分配**或其对应的释放函数）或使用调用标准堆管理器函数的自定义操作的函数。

若要确定是否为程序启用了完全或标准页堆验证，请在命令行中键入**gflags/p**。 在生成的显示中，"**跟踪**" 指示为程序启用了标准页堆验证，而 "**完全跟踪**" 表示为该程序启用了 "完全页堆验证"。

**/Enable**参数为注册表中的映像文件设置[enable page 堆](enable-page-heap.md)（hpa）标志。 但是，在默认情况下， **/enable**参数会为映像文件启用*标准*堆验证，这不同于 **/i**参数和 **+ hpa**标志，后者将为映像文件启用*完全*堆验证。

*标准*页堆验证在分配末尾放置随机模式，并在释放堆块时检查模式。 *整*页堆验证在每次分配结束时放置保留虚拟内存的区域。

整页堆验证可以快速消耗系统内存。 若要为内存密集型进程启用完整页面堆验证，请使用 **/size**或 **/dlls**参数。

使用全局标志进行调试后，提交**gflags/p/disable**命令关闭页堆验证并删除关联的注册表项。 否则，调试器读取的项将保留在注册表中。 不能对此任务使用**gflags/i hpa**命令，因为它会关闭页堆验证，但不会删除注册表项。

默认情况下，在 Windows Vista 和更高版本的 Windows 上，特定于程序的设置（图像文件标志和页面堆验证设置）存储在当前用户帐户中。

此版本的 GFlags 包含 **-v**选项，这将启用为 GFlags 开发的功能。 不过，这些功能尚未完成，因此没有记录。

 

 





