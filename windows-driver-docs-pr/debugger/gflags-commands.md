---
title: GFlags 命令
description: 若要使用 GFlags，请在命令行键入以下命令。 可以交替使用 GFlags 命令和全局标志对话框。
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
ms.openlocfilehash: 7e5d1ea9041b1d4d5fee011516c1f2a1e5a61ea9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370858"
---
# <a name="gflags-command-overview"></a>GFlags 命令概述

有关如何安装和找到 gflags.exe 的常规信息，请参阅[GFlags](gflags.md)。

可以使用 GFlags 命令和[全局标志对话框的](global-flags-dialog-box.md)互换。

## <a name="gflags-command-usage"></a>GFlags 命令的用法 

若要使用 GFlags，请在命令行键入以下命令。


若要打开 GFlags 对话框中：

```console
gflags
```

若要设置或清除在注册表中的全局标志：

```console
gflags /r [{+ | -}Flag [{+ | -}Flag...]]
```

若要设置或清除当前会话的全局标志：

```console
gflags /k [{+ | -}Flag [{+ | -}Flag...]]
```

若要设置或清除的图像文件的全局标志：

```console
gflags /i ImageFile [{+ | -}Flag [{+ | -}Flag...]]
gflags /i ImageFile /tracedb SizeInMB
```

若要设置或清除特殊池功能 (Windows Vista 及更高版本)

```console
gflags {/r | /k} {+ | -}spp {PoolTag | 0xSize}
```

若要启用或禁用的对象引用跟踪功能 (Windows Vista 及更高版本)

```console
gflags {/ro | /ko} [/p] [/i ImageFile | /t PoolTag;[PoolTag...]]
```

```console
gflags {/ro | /ko} /d
```

若要启用和配置页堆验证：

```console
gflags /p /enable ImageFile  [ /full [/backwards] | /random Probability | /size SizeStart SizeEnd | /address AddressStart AddressEnd | /dlls DLL [DLL...] ] 
[/debug ["DebuggerCommand"] | /kdebug] [/unaligned] [/notraces] [/fault Rate [TimeOut]] [/leaks] [/protect] [/no_sync] [/no_lock_checks] 
```

若要禁用页堆验证：

```console
gflags /p [/disable ImageFile] [/?]
```

若要显示帮助：

```console
glags /?
```

## <a name="span-idddk_gflags_commands_dtoolsspanspan-idddk_gflags_commands_dtoolsspanparameters"></a><span id="ddk_gflags_commands_dtools"></span><span id="DDK_GFLAGS_COMMANDS_DTOOLS"></span>参数


<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *Flag*   
指定三字母缩写形式 (*FlagAbbr*) 或十六进制值 (*FlagHex*)，表示一种调试功能。 中列出的缩写和十六进制值[GFlags 标志表](gflags-flag-table.md)。

使用以下标志格式之一：

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
<td align="left"><p>{<strong>+</strong> | <strong>-</strong>}<em>FlagAbbr</em></p></td>
<td align="left"><p>设置 （+） 或清除 （-） 表示的标志缩写的标志。 不带加号 （+） 或减号 （-），该命令不起作用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>[<strong>+</strong> | <strong>-</strong>]<em>FlagHex</em></p></td>
<td align="left"><p>添加 （+） 或十六进制标志的值相减 （-）。 其值包含在 sum 中时设置了标志。 添加 （+） 是默认值。 输入十六进制值 （不带 0 x) 表示的单个标志或输入多个标志的十六进制值的总和。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ImageFile______"></span><span id="_______imagefile______"></span><span id="_______IMAGEFILE______"></span> *ImageFile*   
指定可执行文件，其中包括文件扩展名 （例如，notepad.exe 或 mydll.dll） 的名称。

<span id="________r______"></span><span id="________R______"></span> **/r**   
注册表。 显示或更改存储在注册表中的系统范围内调试标志。 当您重新启动 Windows 并保持有效，直到更改它们，这些设置才会生效。

不带任何其他参数， **gflags /r**显示在注册表中设置的系统范围内标志。

<span id="________k______"></span><span id="________K______"></span> **/k**   
内核标志设置。 显示或更改此会话的系统范围内调试标志。 这些设置将立即生效，但 Windows 关闭时都将丢失。 设置会影响此命令完成后启动的进程。

不带任何其他参数， **gflags /k**显示为当前会话设置的系统范围内标志。

<span id="________i______"></span><span id="________I______"></span> **/i**   
图像文件设置。 显示或更改调试特定进程的标志。 这些设置存储在注册表中。 它们是有效的此过程的所有新实例，它们保持有效，直到更改它们。

不带任何其他参数， **gflags /i** *ImageFile*显示设置为指定的进程的标志。

<span id="________tracedb_______SizeInMB______"></span><span id="________tracedb_______sizeinmb______"></span><span id="________TRACEDB_______SIZEINMB______"></span> **/tracedb** *SizeInMB*   
设置进程的用户模式堆栈跟踪数据库的最大大小。 若要使用此参数，[创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md)(ust) 标志必须设置为该进程。

*SizeInMB*是一个整数，表示以小数单位为兆字节数。 默认值是最小大小 8 MB;没有最大大小。 若要还原到默认大小，则设置*SizeInMB*为 0。

<span id="_______spp______"></span><span id="_______SPP______"></span> **spp**   
(Windows Vista 及更高版本。)设置或清除[特殊池](special-pool.md)功能。 有关示例，请参阅[示例 14:配置特殊池](example-14---configuring-special-pool.md)。

<span id="_______PoolTag______"></span><span id="_______pooltag______"></span><span id="_______POOLTAG______"></span> *PoolTag*   
(Windows Vista 及更高版本。)指定的池标记[特殊池](special-pool.md)功能。 只能用于**spp**标志。

输入的四个字符模式*PoolTag*，例如，标记 1。 它可以包括 **？** （替换为任何单个字符） 和 **\\** * （替换为多个字符） 通配符字符。 例如，Fat\*或 Av？ 4。 池标记始终是区分大小写的。

<span id="0xSize______"></span><span id="0xsize______"></span><span id="0XSIZE______"></span>**0 x * * * 大小*   
(Windows Vista 及更高版本。)指定特殊池功能的大小范围。 只能用于**spp**标志。 选择大小值的指导，请参阅"选择分配大小"中[特殊池](special-pool.md)。

<span id="________ro______"></span><span id="________RO______"></span> **/ro**   
启用、 禁用，并显示[对象引用跟踪](object-reference-tracing.md)注册表中的设置。 若要使此设置更改生效，必须重新启动 Windows。

不使用其他参数 **/ro**在注册表中显示的对象引用跟踪设置。

若要启用对象引用跟踪，必须包含至少一个池标记 ( **/t** *PoolTag*) 或一个图像文件 ( **/i** ImageFile) 命令中。 有关详细信息，请参阅[示例 15:使用对象引用跟踪](example-15--using-object-reference-tracing.md)。

下表列出了使用有效的子参数均 **/ro**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/t</strong> <em>PoolTags</em></p></td>
<td align="left"><p>限制跟踪到具有指定的池标记的对象。 使用分号 (<strong>;</strong>) 来分隔标记名称。 输入最多 16 个池标记。</p>
<p>输入的四个字符模式<em>PoolTags</em>，例如，标记 1。</p>
<p>如果指定多个池标记时，Windows 将跟踪与任何指定的池标记的对象。</p>
<p>如果不指定任何池标记，Windows 将跟踪的映像创建的所有对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong> <em>ImageFile</em></p></td>
<td align="left"><p>限制跟踪到与指定的图像文件创建的进程对象。 可以指定只有一个图像文件<strong>/i</strong>参数。</p>
<p>输入图像文件名称，如 notepad.exe，最多 64 个字符。 "系统"和"空闲"不是有效的图像名称。</p>
<p>如果不指定图像文件，Windows 将跟踪与指定的池标记的所有对象。 如果指定这两个图像文件 (<strong>/i</strong>) 和一个或多个池标记 (<strong>/t</strong>)，Windows 跟踪与任何指定的映像创建的指定的池标记的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/d</strong></p></td>
<td align="left"><p>清除对象引用跟踪功能设置。 与一起使用时<strong>/ro</strong>，它会清除注册表中的设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>永久。 对象引用跟踪处于禁用状态，或关闭或重新启动计算机之前，将保留的跟踪数据。 默认情况下，当对象被销毁时丢弃的对象的跟踪数据。</p></td>
</tr>
</tbody>
</table>

 

<span id="________ko______"></span><span id="________KO______"></span> **/ko**   
启用、 禁用，并显示 （运行时间） 的内核标志[对象引用跟踪](object-reference-tracing.md)设置。 更改此设置将立即生效，但当系统关闭或重新启动时都将丢失。 有关详细信息，请参阅[示例 15:使用对象引用跟踪](example-15--using-object-reference-tracing.md)。

不使用其他参数 **/ko**显示内核标志 （运行时间） 对象引用跟踪设置。

若要启用对象引用跟踪，必须包含至少一个池标记 ( **/t** *PoolTag*) 或一个图像文件 ( **/i** *ImageFile*) 中该命令。

下表列出了使用有效的子参数均 **/ko**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>/t</strong> <em>PoolTags</em></p></td>
<td align="left"><p>限制跟踪到具有指定的池标记的对象。 使用分号 (<strong>;</strong>) 来分隔标记名称。 输入最多 16 个池标记。</p>
<p>输入的四个字符模式<em>PoolTags</em>，例如，标记 1。</p>
<p>如果指定多个池标记时，Windows 将跟踪与任何指定的池标记的对象。</p>
<p>如果不指定任何池标记，Windows 将跟踪的映像创建的所有对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/i</strong> <em>ImageFile</em></p></td>
<td align="left"><p>限制跟踪到与指定的图像文件创建的进程对象。 可以指定只有一个图像文件<strong>/i</strong>参数。</p>
<p>如果不指定图像文件，Windows 将跟踪与指定的池标记的所有对象。</p>
<p>如果指定这两个图像文件 (<strong>/i</strong>) 和一个或多个池标记 (<strong>/t</strong>)，Windows 跟踪与任何指定的映像创建的指定的池标记的对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>/d</strong></p></td>
<td align="left"><p>清除对象引用跟踪功能设置。 与一起使用时<strong>/ro</strong>，它会清除注册表中的设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>/p</strong></p></td>
<td align="left"><p>永久。 对象引用跟踪处于禁用状态，或关闭或重新启动计算机之前，将保留的跟踪数据。 默认情况下，当对象被销毁时丢弃的对象的跟踪数据。</p></td>
</tr>
</tbody>
</table>

 

<span id="________p______"></span><span id="________P______"></span> **/p**   
设置页面的进程堆验证选项。

不带任何其他参数， **gflags/p**显示堆验证启用的哪一页的图像文件的列表。

页堆验证监视器动态堆内存操作，包括分配操作和 free 操作，并且检测到堆错误时，会导致调试器中断。

<span id="________disable_______ImageFile______"></span><span id="________disable_______imagefile______"></span><span id="________DISABLE_______IMAGEFILE______"></span> **/disable** *ImageFile*   
关闭页堆验证 （标准版或完整） 指定的图像文件。

此命令相当于关闭[启用页堆](enable-page-heap.md)进程 (hpa) 标志 (**gflags /i** *ImageFile* **-hpa**)。 你可以交替使用这些命令。

<span id="________enable_______ImageFile______"></span><span id="________enable_______imagefile______"></span><span id="________ENABLE_______IMAGEFILE______"></span> **/enable** *ImageFile*   
打开指定的图像文件的页堆验证。

默认情况下 **/ 启用**参数打开*标准*页上的图像文件的堆验证。 若要启用*完整*页上的图像文件的堆验证，添加 **/完整**命令或使用的参数 **/i**参数 **+ hpa**标志。

<span id="________full______"></span><span id="________FULL______"></span> **/full**   
打开的进程的整页堆验证。 整页堆验证将在每次分配结束位置的区域的保留虚拟内存。

使用此参数等效于开启[启用页堆](enable-page-heap.md)进程 (hpa) 标志 (**gflags /i** *ImageFile* **+ hpa**)。 你可以交替使用这些命令。

<span id="________backwards______"></span><span id="________BACKWARDS______"></span> **/backwards**   
在开始分配，而不是结束时，请将保留虚拟内存的区域。 因此，调试器捕获溢出缓冲区，而不是在缓冲区末尾的开始处。 仅对于有效 **/full**参数。

<span id="________random_______Probability______"></span><span id="________random_______probability______"></span><span id="________RANDOM_______PROBABILITY______"></span> **/ 随机***概率*   
选择每个分配时，根据指定的概率的完整或标准页堆验证。

*概率*是十进制整数 0 到 100 表示的整页堆验证概率。 100 的概率是使用相同 **/full**参数。 0 的概率是使用标准页面堆验证相同。

<span id="________size________SizeStart_SizeEnd______"></span><span id="________size________sizestart_sizeend______"></span><span id="________SIZE________SIZESTART_SIZEEND______"></span> **/size** *SizeStart SizeEnd*   
启用指定的大小范围内分配的整页堆验证并启用标准页对于所有其他分配的堆验证进程。

*SizeStart*并*SizeEnd*是十进制整数。 默认值为所有分配的标准页面堆验证。

<span id="________address________AddressStart_AddressEnd______"></span><span id="________address________addressstart_addressend______"></span><span id="________ADDRESS________ADDRESSSTART_ADDRESSEND______"></span> **/address** *AddressStart AddressEnd*   
启用指定的地址范围中的返回地址时分配的内存整页堆验证是在运行时调用堆栈。 这样，对于所有其他分配的标准页面堆验证进程。

若要使用此功能，指定包括的所有函数的调用带有可疑的分配函数的地址范围。 可疑的分配发生时，调用函数的地址将在调用堆栈上。

*AddressStart*并*AddressEnd*指定分配堆栈跟踪中搜索的地址范围。 以十六进制格式，如 0xAABBCCDD 已指定的地址。

在 Windows Server 2003 和早期系统上 **/地址**参数是仅对有效*x*86 基于计算机。 在 Windows Vista： 上是有效的所有受支持的体系结构上。

<span id="________dlls_DLL___DLL...__"></span><span id="________dlls_dll___dll...__"></span><span id="________DLLS_DLL___DLL...__"></span> **/dlls** *DLL*\[ **,** *DLL*...\]   
启用整页堆验证用于分配请求指定的 Dll 和进程的所有其他分配的标准页面堆验证。

*DLL*是二进制文件，包括其文件扩展名的名称。 指定的文件必须是该进程在执行期间加载的函数库。

<span id="________debug______"></span><span id="________DEBUG______"></span> **/debug**   
指定的进程将自动启动 **/ 启用**在调试器下的参数。

默认情况下，此参数会使用命令行使用的是 NTSD 调试器**ntsd-g-G-x**和与页堆启用，但你可以使用*DebuggerCommand*变量以指定不同的调试器和命令行。

NTSD 有关的信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

此选项可用于很难从命令提示符并启动其他进程启动的程序。

<span id="_DebuggerCommand_______"></span><span id="_debuggercommand_______"></span><span id="_DEBUGGERCOMMAND_______"></span> **"** <em>DebuggerCommand</em> **"**    
指定调试程序和发送到调试器的命令。 带引号的字符串这可能包括调试器，调试程序名称和调试器将解释的命令参数的完全限定的路径。 需要引号。

如果该命令包含在调试器的路径，路径不能包含其他任何引号。 如果其他引号出现，命令行界面 (*cmd.exe*) 将解释该命令。

<span id="________kdebug______"></span><span id="________KDEBUG______"></span> **/kdebug**   
指定的进程将自动启动 **/ 启用**下的是 NTSD 调试器使用命令行参数**ntsd-g-G-x**、 启用，页面堆和 NTSD 重定向到的控件内核调试程序。

NTSD 有关的信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

<span id="________unaligned______"></span><span id="________UNALIGNED______"></span> **/unaligned**   
即使这样做意味着起始地址未对齐的 8 字节块上对齐每个分配在结束页边界的末尾。 默认情况下，堆管理器可保证一个 8 字节块对齐的分配的起始地址。

此选项用于检测关闭一个字节的错误。 当此参数用于 **/完整**参数之后分配的最后一个字节, 开始的保留虚拟内存区域，并且进程试图读取或写入甚至一个字节超出时发生即时错误分配。

<span id="________decommit______"></span><span id="________DECOMMIT______"></span> **/decommit**   
此选项将不再有效。 它接受，但被忽略。

在 Windows 2000 中包含的 PageHeap 程序 (pageheap.exe) 上来分配后将无法访问页实现整页堆验证。 在该工具中， **/ 解除**参数替换的区域的保留的无法访问页上的虚拟内存。 在此版本的 GFlags，保留虚拟内存区域始终用于实现整页堆验证。

<span id="________notraces______"></span><span id="________NOTRACES______"></span> **/notraces**   
指定运行时堆栈跟踪不会保存。

此选项可以提高性能略有不同，但它使得调试更加困难。 此参数才有效，但不是建议使用。

<span id="________fault______"></span><span id="________FAULT______"></span> **/fault**   
强制该程序的内存分配失败以指定的速率和指定的超时之后。

此参数将插入堆分配错误到所测试的图像文件 （此做法称为"故障注入"） 因此，某些内存分配会失败，因为可能会出现内存不足的情况中运行程序时。 此测试可帮助检测中处理分配失败，如无法释放资源的错误。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><em>速率</em></p></td>
<td align="left"><p>指定从 1 十进制整数 (。 01%)通过 10000 （100%)表示分配会失败的概率。 默认值为 100 （1%)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>TimeOut</em></p></td>
<td align="left"><p>确定启动程序的故障注入例程开始之间的时间间隔。</p>
<p><em>超时</em>以秒为单位。 默认值为 5 （秒）。</p></td>
</tr>
</tbody>
</table>

 

<span id="________leaks______"></span><span id="________LEAKS______"></span> **/leaks**   
检查堆泄漏处理结束时。

**泄漏/** 参数禁用整个页面堆栈。 时 **/泄漏**使用，则 **/full**参数和参数，修改 **/完整**参数，如 **/ 向后**，将被忽略，和 GFlags 执行泄漏检查使用的标准页面堆验证。

<span id="________protect______"></span><span id="________PROTECT______"></span> **/protect**   
保护堆内部结构。 此测试用于检测随机堆损坏。 它会使执行速度慢得多。

<span id="________no_sync______"></span><span id="________NO_SYNC______"></span> **/no\_sync**   
对于不同步访问检查。 此参数，会导致中断如果它检测到的堆创建与堆\_否\_由不同的线程访问序列化标志。

不要使用此标志进行调试的程序包含自定义的堆管理器。 同步堆的访问的函数会导致到不存在的报表同步错误的页堆验证程序。

<span id="________no_lock_checks______"></span><span id="________NO_LOCK_CHECKS______"></span> **/no\_lock\_checks**   
禁用关键部分验证程序。

<span id="_______________"></span> **/?**    
显示有关 GFlags 帮助。 与 **/p**， **/？** 显示在 GFlags 页面堆验证选项的帮助。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

键入**gflags**没有参数打开**全局标志**对话框。

键入**gflags/p**没有其他参数显示已启用页堆验证程序的列表。

若要清除所有标志，请设置*标志*到 **-FFFFFFFF**。 (设置*标志*为 0 将添加到当前的标志值零。 它不会清除所有标志。）

当您将设置*标志*到图像文件**FFFFFFFF**，Windows 清除所有标志 GlobalFlag，项并删除该图像文件的注册表子项中。 将保持该子项。

**/Full**， **/ 随机**， **/大小**， **/地址**，并 **/dlls**页堆参数 **/ 启用**操作确定哪些分配可能会有所页堆验证和使用的验证方法。 可以在每个命令使用以下参数之一。 默认为标准页的过程的所有分配的堆验证。 剩余的参数设置页堆验证选项。

GFlags 中的页堆功能只监视使用标准 Windows 堆管理器函数的堆内存分配 (**HeapAlloc**， **GlobalAlloc**， **LocalAlloc**，**malloc**，**新**，**新\[\]** ，或解除分配的函数及其相应)，或使用自定义操作调用标准堆管理器函数。

若要确定是否启用了完整或标准页堆验证程序，在命令行中，键入**gflags/p**。 在生成的显示中，**跟踪**指示标准页面堆验证已启用程序和**完整跟踪**指示为程序启用了整页堆验证。

**/ 启用**参数集[启用页堆](enable-page-heap.md)注册表中的图像文件 (hpa) 标志。 但是， **/ 启用**参数打开*标准*不同于默认情况下，堆的图像文件的验证 **/i**参数 **+ hpa**标志，开启*完整*堆的图像文件的验证。

*标准*页堆验证会随机模式放在末尾的分配和释放堆块时检查这些模式。 *完整*页堆验证将在每次分配结束的位置的区域的保留虚拟内存。

整页堆验证可以快速使用的系统内存。 若要启用的占用大量内存的进程的整页堆验证，请使用 **/大小**或 **/dlls**参数。

使用全局标志进行调试之后, 提交**gflags/p /disable**命令来关闭页堆验证并删除关联的注册表项。 否则，调试器读取的项保留在注册表中。 不能使用**gflags /i hpa**命令对于此任务，因为它会关闭页堆验证，但不会删除注册表项。

默认情况下，Windows Vista 和更高版本的 Windows，特定于程序的设置 （图像文件标志和页堆验证设置） 存储在当前的用户帐户。

包括此版本的 GFlags **-v**选项，以允许为 GFlags 正在开发的功能。 但是，这些功能仍未完成，因此，未记录。

 

 





