---
title: 符号选项
description: 符号选项
ms.assetid: 4a501ea3-431c-4c11-8826-154eb8799a64
keywords:
- 符号设置符号选项
- 符号 SYMOPT_XXXX
- 干扰符号加载
- CV 记录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9832b751affe05bd31977c0a82280a3e2f692e7b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335515"
---
# <a name="symbol-options"></a>符号选项


## <span id="ddk_setting_symbol_options_dbg"></span><span id="DDK_SETTING_SYMBOL_OPTIONS_DBG"></span>


有多种选项都是可用于控制如何加载和使用的符号。 可以在不同的方式设置这些选项。

下表列出了这些符号选项：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">选项名称</th>
<th align="left">调试器中的默认值</th>
<th align="left">DBH 中的默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p><a href="#symopt-case-insensitive" data-raw-source="[SYMOPT_CASE_INSENSITIVE](#symopt-case-insensitive)">SYMOPT_CASE_INSENSITIVE</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p><a href="#symopt-undname" data-raw-source="[SYMOPT_UNDNAME](#symopt-undname)">SYMOPT_UNDNAME</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p><a href="#symopt-deferred-loads" data-raw-source="[SYMOPT_DEFERRED_LOADS](#symopt-deferred-loads)">SYMOPT_DEFERRED_LOADS</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p><a href="#symopt-no-cpp" data-raw-source="[SYMOPT_NO_CPP](#symopt-no-cpp)">SYMOPT_NO_CPP</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p><a href="#symopt-load-lines" data-raw-source="[SYMOPT_LOAD_LINES](#symopt-load-lines)">SYMOPT_LOAD_LINES</a></p></td>
<td align="left"><p>关闭 KD 和 CDB 中</p>
<p>在 WinDbg 中</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p><a href="#symopt-omap-find-nearest" data-raw-source="[SYMOPT_OMAP_FIND_NEAREST](#symopt-omap-find-nearest)">SYMOPT_OMAP_FIND_NEAREST</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p><a href="#symopt-load-anything" data-raw-source="[SYMOPT_LOAD_ANYTHING](#symopt-load-anything)">SYMOPT_LOAD_ANYTHING</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80</p></td>
<td align="left"><p><a href="#symopt-ignore-cvrec" data-raw-source="[SYMOPT_IGNORE_CVREC](#symopt-ignore-cvrec)">SYMOPT_IGNORE_CVREC</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100</p></td>
<td align="left"><p><a href="#symopt-no-unqualified-loads" data-raw-source="[SYMOPT_NO_UNQUALIFIED_LOADS](#symopt-no-unqualified-loads)">SYMOPT_NO_UNQUALIFIED_LOADS</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p><a href="#symopt-fail-critical-errors" data-raw-source="[SYMOPT_FAIL_CRITICAL_ERRORS](#symopt-fail-critical-errors)">SYMOPT_FAIL_CRITICAL_ERRORS</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p><a href="#symopt-exact-symbols" data-raw-source="[SYMOPT_EXACT_SYMBOLS](#symopt-exact-symbols)">SYMOPT_EXACT_SYMBOLS</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p><a href="#symopt-allow-absolute-symbols" data-raw-source="[SYMOPT_ALLOW_ABSOLUTE_SYMBOLS](#symopt-allow-absolute-symbols)">SYMOPT_ALLOW_ABSOLUTE_SYMBOLS</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p><a href="#symopt-ignore-nt-sympath" data-raw-source="[SYMOPT_IGNORE_NT_SYMPATH](#symopt-ignore-nt-sympath)">SYMOPT_IGNORE_NT_SYMPATH</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2000</p></td>
<td align="left"><p>SYMOPT_INCLUDE_32BIT_MODULES</p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4000</p></td>
<td align="left"><p><a href="#symopt-publics-only" data-raw-source="[SYMOPT_PUBLICS_ONLY](#symopt-publics-only)">SYMOPT_PUBLICS_ONLY</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8000</p></td>
<td align="left"><p><a href="#symopt-no-publics" data-raw-source="[SYMOPT_NO_PUBLICS](#symopt-no-publics)">SYMOPT_NO_PUBLICS</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10000</p></td>
<td align="left"><p><a href="#symopt-auto-publics" data-raw-source="[SYMOPT_AUTO_PUBLICS](#symopt-auto-publics)">SYMOPT_AUTO_PUBLICS</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>开</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000</p></td>
<td align="left"><p><a href="#symopt-no-image-search" data-raw-source="[SYMOPT_NO_IMAGE_SEARCH](#symopt-no-image-search)">SYMOPT_NO_IMAGE_SEARCH</a></p></td>
<td align="left"><p>开</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000</p></td>
<td align="left"><p><a href="#symopt-secure" data-raw-source="[SYMOPT_SECURE](#symopt-secure)">SYMOPT_SECURE</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000</p></td>
<td align="left"><p><a href="#symopt-no-prompts" data-raw-source="[SYMOPT_NO_PROMPTS](#symopt-no-prompts)">SYMOPT_NO_PROMPTS</a></p></td>
<td align="left"><p>在中 KD 和 CDB</p>
<p>在 WinDbg 中关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p><a href="#symopt-debug" data-raw-source="[SYMOPT_DEBUG](#symopt-debug)">SYMOPT_DEBUG</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>关闭</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idchanging-the-symbol-option-settingsspanspan-idchangingthesymboloptionsettingsspanchanging-the-symbol-option-settings"></a><span id="changing-the-symbol-option-settings"></span><span id="CHANGING_THE_SYMBOL_OPTION_SETTINGS"></span>更改符号选项设置

[ **.Symopt （设置符号选项）** ](-symopt--set-symbol-options-.md)命令可用于更改或显示符号选项设置。 此外，有多种命令行参数和命令都是可用于更改这些设置;所示单个 SYMOPT\_*XXX*部分。

您还可以控制一次性使用的所有设置 **-sflags**[命令行选项](command-line-options.md)。 此选项可后接一个十进制数，或为前缀的十六进制数**0x**。 建议使用十六进制格式，因为符号标志正确对齐这种方式。 使用此方法，因为它将整个位域，并将替代所有符号处理程序默认值时要小心。 例如， **-sflags 0x401**将只启用的 SYMOPT\_EXACT\_符号和 SYMOPT\_用例\_INSENSITIVE，但将还关闭所有其他选项，方法通常是上默认值 ！

总标志位的默认值是在 WinDbg 中的 0x30237、 CDB 和 KD，0xB0227 和中的 0x10C13 [DBH 工具](dbh.md)，当不使用任何与符号相关的命令行选项启动这些程序。

### <a name="span-idsymopt-case-insensitivespanspan-idsymoptcaseinsensitivespansymoptcaseinsensitive"></a><span id="symopt-case-insensitive"></span><span id="SYMOPT_CASE_INSENSITIVE"></span>SYMOPT\_CASE\_INSENSITIVE

此符号选项将导致所有搜索符号名称不区分大小写。

此选项是在默认情况下，所有调试器中。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x1**或.symopt 0x1，分别。

此选项位于 DBH 默认情况下。 DBH 开始运行后，它可以打开或关闭分别使用 symopt + 1 或-1，symopt。

### <a name="span-idsymopt-undnamespanspan-idsymoptundnamespansymoptundname"></a><span id="symopt-undname"></span><span id="SYMOPT_UNDNAME"></span>SYMOPT\_UNDNAME

此符号选项会使公共符号名称以显示，并且会导致搜索要忽略符号修饰的符号名称时，会未修饰。 私有符号名永远不会进行修饰，而不考虑此选项是否处于活动状态。 符号名称修饰的信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

此选项是在默认情况下，所有调试器中。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x2**或.symopt 0x2，分别。

此选项位于 DBH 默认情况下。 如果使用-d 的命令行选项，则它处于关闭状态。 DBH 开始运行后，它可以打开或关闭使用 symopt + 2 或 symopt-2，分别。

### <a name="span-idsymopt-deferred-loadsspanspan-idsymoptdeferredloadsspansymoptdeferredloads"></a><span id="symopt-deferred-loads"></span><span id="SYMOPT_DEFERRED_LOADS"></span>SYMOPT\_延期\_加载

此符号选项称为*延迟的符号加载*或*延迟符号加载*。 当它处于活动状态时，符号不会实际加载时加载目标模块。 相反，符号进行加载由调试器需要它们。 请参阅[延迟的符号加载](deferred-symbol-loading.md)有关详细信息。

此选项是在默认情况下，所有调试器中。 在 CDB 和 KD，-s 命令行选项将关闭此选项。 它可以也关闭 CDB 中通过使用**LazyLoad**变量中[tools.ini](configuring-tools-ini.md)文件。 调试器开始运行后，此选项可以打开或关闭通过使用 **.symopt + 0x4**或.symopt 0x4，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 4 或 symopt-4。

### <a name="span-idsymopt-no-cppspanspan-idsymoptnocppspansymoptnocpp"></a><span id="symopt-no-cpp"></span><span id="SYMOPT_NO_CPP"></span>SYMOPT\_NO\_CPP

此符号选项将关闭C++转换。 当设置此符号选项时， **::** 替换为**\_ \_** 中所有的符号。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 使用-snc 命令行选项，可以激活它。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x8**或.symopt 0x8，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 8 或 symopt-8。

### <a name="span-idsymopt-load-linesspanspan-idsymoptloadlinesspansymoptloadlines"></a><span id="symopt-load-lines"></span><span id="SYMOPT_LOAD_LINES"></span>SYMOPT\_负载\_行

此符号选项允许从源代码文件中读取的行号信息。 此选项必须位于源调试才能正常工作。

在 KD 和 CDB 中，此选项默认处于关闭状态;在 WinDbg 中，此选项是在默认情况下。 在 CDB 和 KD，命令行选项将启用此选项的行。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x10**或.symopt 0x10，分别。 它还可以打开和关闭使用[ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令。

此选项位于 DBH 默认情况下。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 10 或 symopt-10。

### <a name="span-idsymopt-omap-find-nearestspanspan-idsymoptomapfindnearestspansymoptomapfindnearest"></a><span id="symopt-omap-find-nearest"></span><span id="SYMOPT_OMAP_FIND_NEAREST"></span>SYMOPT\_OMAP\_FIND\_NEAREST

当代码已经过优化，并且在预期位置没有出现任何符号时，该选项将使要改为使用的最接近的符号。

此选项是在默认情况下，所有调试器中。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x20**或.symopt 0x20，分别。

此选项位于 DBH 默认情况下。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 20 或 symopt-20。

### <a name="span-idsymopt-load-anythingspanspan-idsymoptloadanythingspansymoptloadanything"></a><span id="symopt-load-anything"></span><span id="SYMOPT_LOAD_ANYTHING"></span>SYMOPT\_负载\_ANYTHING

当它尝试匹配符号时，此符号选项可减少符号处理程序的 pickiness。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x40**或.symopt 0x40，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt 40 或 symopt-40。

### <a name="span-idsymopt-ignore-cvrecspanspan-idsymoptignorecvrecspansymoptignorecvrec"></a><span id="symopt-ignore-cvrec"></span><span id="SYMOPT_IGNORE_CVREC"></span>SYMOPT\_忽略\_CVREC

此符号选项会导致要搜索的符号时忽略 CV 记录加载的映像标头中的符号处理程序。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 可以通过使用-sicv 命令行选项来激活它。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x80**或.symopt 0x80，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 80 或 symopt-80。

### <a name="span-idsymopt-no-unqualified-loadsspanspan-idsymoptnounqualifiedloadsspansymoptnounqualifiedloads"></a><span id="symopt-no-unqualified-loads"></span><span id="SYMOPT_NO_UNQUALIFIED_LOADS"></span>SYMOPT\_否\_UNQUALIFIED\_加载

此符号选项禁用符号处理程序的自动加载模块。 如果设置此选项，调试器会尝试匹配一个符号，它将仅搜索已加载的模块。

此选项可以用作防御符号名称键入错误。 通常情况下，出现输入错误的符号将导致调试器暂停时它会搜索所有已卸载的符号文件。 时此选项处于活动状态，在加载的模块中，将不会找到错误输入的符号，然后搜索将终止。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 可以通过使用-snul 命令行选项来激活它。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x100**或.symopt 0x100，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 100 或 symopt-100。

### <a name="span-idsymopt-fail-critical-errorsspanspan-idsymoptfailcriticalerrorsspansymoptfailcriticalerrors"></a><span id="symopt-fail-critical-errors"></span><span id="SYMOPT_FAIL_CRITICAL_ERRORS"></span>SYMOPT\_失败\_严重\_错误

此符号选项将导致文件访问错误对话框来禁止显示。

如果此选项处于关闭状态，文件访问错误，例如"驱动器未就绪"符号加载过程中遇到会导致出现的对话框。 如果已启用此选项，这些框会抑制和访问的所有错误都收到"失败"响应。

此选项是在默认情况下，所有调试器中。 它可以被停用使用-sdce 命令行选项。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x200**或.symopt 0x200，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt + 200 或 symopt-200。

### <a name="span-idsymopt-exact-symbolsspanspan-idsymoptexactsymbolsspansymoptexactsymbols"></a><span id="symopt-exact-symbols"></span><span id="SYMOPT_EXACT_SYMBOLS"></span>SYMOPT\_EXACT\_符号

此符号选项会导致调试器执行的所有符号文件严格评估。

在此选项时，甚至之间的符号文件和符号处理程序的预期的最小差异会导致符号被忽略。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 可以通过使用-ses 命令行选项来激活它。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x400**或.symopt 0x400，分别。

-Failinc 命令行选项也可启用 SYMOPT\_EXACT\_符号。 此外，如果你正在调试小型转储用户模式或内核模式小型转储，-failinc 将阻止调试器加载任何模块不能映射其映像。

此选项位于 DBH 默认情况下。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +400 或 symopt-400。

### <a name="span-idsymopt-allow-absolute-symbolsspanspan-idsymoptallowabsolutesymbolsspansymoptallowabsolutesymbols"></a><span id="symopt-allow-absolute-symbols"></span><span id="SYMOPT_ALLOW_ABSOLUTE_SYMBOLS"></span>SYMOPT\_允许\_绝对\_符号

此符号选项允许 DbgHelp 读取存储在内存中的绝对地址的符号。 在大多数情况下不需要此选项。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x800**或.symopt 0x800，分别。

此选项位于 DBH 默认情况下。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt 将 800 多或 symopt-800。

### <a name="span-idsymopt-ignore-nt-sympathspanspan-idsymoptignorentsympathspansymoptignorentsympath"></a><span id="symopt-ignore-nt-sympath"></span><span id="SYMOPT_IGNORE_NT_SYMPATH"></span>SYMOPT\_忽略\_NT\_SYMPATH

此符号选项会导致调试器忽略符号路径和可执行映像路径的环境变量设置。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 可以通过使用-sins 命令行选项来激活它。 但是，它不能控制 **.symopt**调试器开始运行后，因为在启动时才读取环境变量。

此选项在 DBH，默认情况下处于关闭状态，并且在所有情况下 DBH 被忽略。

### <a name="span-idsymopt-publics-onlyspanspan-idsymoptpublicsonlyspansymoptpublicsonly"></a><span id="symopt-publics-only"></span><span id="SYMOPT_PUBLICS_ONLY"></span>SYMOPT\_PUBLICS\_仅

此符号选项将导致 DbgHelp 忽略私有符号数据，并搜索仅公共符号表中的符号信息。 这是这些类型已添加对模拟 DbgHelp 之前支持的行为。 请参阅[公共和私有符号](public-and-private-symbols.md)。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x4000**或.symopt 0x4000，分别。

DBH 中默认情况下，此选项处于关闭状态。 它被打开如果使用-d 的命令行选项。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +4000 或 symopt-4000。

### <a name="span-idsymopt-no-publicsspanspan-idsymoptnopublicsspansymoptnopublics"></a><span id="symopt-no-publics"></span><span id="SYMOPT_NO_PUBLICS"></span>SYMOPT\_否\_PUBLICS

此符号选项禁止 DbgHelp 搜索公共符号表。 这会使 symbol 枚举和符号搜索要快得多。 如果您担心仅搜索速度，SYMOPT\_自动\_PUBLICS 选项更通常适合于此。 有关公共符号表的信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x8000**或.symopt 0x8000，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +8000 或 symopt-8000。

### <a name="span-idsymopt-auto-publicsspanspan-idsymopt-auto-publicsspansymoptautopublics"></a><span id="symopt-auto-publics"></span><span id="SYMOPT-AUTO-PUBLICS"></span>SYMOPT\_自动\_PUBLICS

此符号选项将导致 DbgHelp 公共符号表中仅作为最后的手段的.pdb 文件中搜索。 如果找到任何匹配项搜索中的私有符号数据时，将不搜索公共符号。 这提高了符号搜索速度。

此选项是在默认情况下，所有调试器中。 它可以通过使用停用-s u p 命令行选项。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x10000**或.symopt 0x10000，分别。

此选项位于 DBH 默认情况下。 如果使用-d 的命令行选项，则它处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +10000 或 symopt-10000。

### <a name="span-idsymopt-no-image-searchspanspan-idsymopt-no-image-searchspansymoptnoimagesearch"></a><span id="symopt-no-image-search"></span><span id="SYMOPT-NO-IMAGE-SEARCH"></span>SYMOPT\_否\_映像\_搜索

此符号选项禁止 DbgHelp 在加载符号时搜索的磁盘映像的副本。

此选项是在默认情况下，所有调试器中。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x20000**或.symopt 0x20000，分别。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +20000 或 symopt-20000。

### <a name="span-idsymopt-securespanspan-idsymoptsecurespansymoptsecure"></a><span id="symopt-secure"></span><span id="SYMOPT_SECURE"></span>SYMOPT\_安全

（仅适用于内核模式）此符号选项指示是否[安全模式下](secure-mode.md)处于活动状态。

默认情况下，在所有调试器情况下，安全模式下处于关闭状态。 它可以通过使用激活-安全的命令行选项。 如果调试器正在运行，是在休眠模式下，未建立任何调试服务器，可以通过打开安全模式下 **.symopt + 而 0x40000 可**或[ **.secure （激活安全模式）**](-secure--activate-secure-mode-.md).

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +40000 或 symopt-40000。

安全模式下可以永远不会关闭后激活它。

### <a name="span-idsymopt-no-promptsspanspan-idsymoptnopromptsspansymoptnoprompts"></a><span id="symopt-no-prompts"></span><span id="SYMOPT_NO_PROMPTS"></span>SYMOPT\_否\_提示

此符号选项禁止显示来自代理服务器的身份验证对话框。 这可能会导致 SymSrv 无法访问 internet 的符号存储区。

有关详细信息，请参阅[防火墙和代理服务器](firewalls-and-proxy-servers.md)。

在 KD 和 CDB 中，此选项位于默认设置。在 WinDbg 中，此选项默认处于关闭状态。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x80000**或.symopt 0x80000，分别跟[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令。 它可以也已打开和关闭使用[ **！ 符号提示关闭**](-sym.md)并 **！ 符号提示**扩展命令后, 跟 **.reload （重新加载模块）** 命令。

DBH 中默认情况下，此选项处于关闭状态。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +80000 或 symopt-80000。

### <span id="symopt-disable-fast-symbols"></span>

### <span id="symopt_disable_symsrv_timeout"></span>

### <a name="span-idsymopt-debugspan-symoptdebug"></a><span id="symopt-debug"></span>-SYMOPT\_DEBUG

此符号选项开启*干扰符号加载*。 这会指示调试器以显示有关其搜索符号信息。

在加载它时，将显示每个符号文件的名称。 如果调试器无法加载符号文件，它将显示一条错误消息。 .Pdb 文件的错误消息将以文本显示。 .Dbg 文件的错误消息将被形式的错误代码;在 winerror.h 文件中介绍了这些代码。

如果加载的图像文件只是为了恢复符号标头信息，这将还显示。

默认情况下，在所有调试器情况下，此选项处于关闭状态。 可以通过使用-n 命令行选项来激活它。 调试器开始运行后，它可以打开或关闭通过使用 **.symopt + 0x80000000**或.symopt 0x80000000，分别。 可以还通过启用和禁用通过使用[ **！ 符号干扰性**](-sym.md)并 **！ 符号静默**扩展命令。

**请注意**  不将此选项与干扰性相混淆*源*加载-由控制[ **（干扰源加载） 可通过.srcnoisy** ](-srcnoisy--noisy-source-loading-.md)命令。

 

DBH 中默认情况下，此选项处于关闭状态。 可以通过使用-n 命令行选项来激活它。 DBH 开始运行后，它可以打开或关闭通过分别使用 symopt +80000000 或 symopt-80000000。 它可以也已打开和关闭使用详细上和 verbose 关闭命令。

 

 





