---
title: 符号选项
description: 符号选项
ms.assetid: 4a501ea3-431c-4c11-8826-154eb8799a64
keywords:
- 符号，设置符号选项
- 符号，SYMOPT_XXXX
- 干扰符号加载
- CV 记录
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9832b751affe05bd31977c0a82280a3e2f692e7b
ms.sourcegitcommit: 89b8a43480246dd726e3632aab2db9cf2eb7505d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2020
ms.locfileid: "92254062"
---
# <a name="symbol-options"></a>符号选项


## <span id="ddk_setting_symbol_options_dbg"></span><span id="DDK_SETTING_SYMBOL_OPTIONS_DBG"></span>


有许多选项可用于控制如何加载和使用符号。 可以通过多种方式设置这些选项。

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
<th align="left">标志</th>
<th align="left">选项名称</th>
<th align="left">调试器中的默认值</th>
<th align="left">THIS->DBH 中的默认值</th>
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
<td align="left"><p>在 KD 和 CDB 中关闭</p>
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
<td align="left"><p>启用</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p><a href="#symopt-allow-absolute-symbols" data-raw-source="[SYMOPT_ALLOW_ABSOLUTE_SYMBOLS](#symopt-allow-absolute-symbols)">SYMOPT_ALLOW_ABSOLUTE_SYMBOLS</a></p></td>
<td align="left"><p>关闭</p></td>
<td align="left"><p>启用</p></td>
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
<td align="left"><p>在 KD 和 CDB 中</p>
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

 

### <a name="span-idchanging-the-symbol-option-settingsspanspan-idchanging_the_symbol_option_settingsspanchanging-the-symbol-option-settings"></a><span id="changing-the-symbol-option-settings"></span><span id="CHANGING_THE_SYMBOL_OPTION_SETTINGS"></span>更改符号选项设置

[**Symopt (设置符号选项) **](-symopt--set-symbol-options-.md)命令可用于更改或显示符号选项设置。 此外，还可以使用多个命令行参数和命令来更改这些设置;各个 SYMOPT XXX 部分中列出了这些 \_ *XXX*内容。

还可以通过 **-sflags**[命令行选项](command-line-options.md)一次性控制所有设置。 此选项的后面可以是十进制数字，也可以是前缀为 **0x**的十六进制数。 建议使用十六进制，因为符号标志以这种方式正确对齐。 使用此方法时要格外小心，因为它会设置整个位域并将覆盖所有符号处理程序默认值。 例如， **-sflags 0x401** 不仅会启用 SYMOPT \_ 精确符号，而且不 \_ \_ 区分大小写 \_ ，还会关闭通常默认启用的所有其他选项！

如果在没有任何符号相关的命令行选项的情况下启动这些程序，则 total 标志位的默认值将在 WinDbg 中0x30237、在 CDB 和 KD 中为0xB0227，在 [this->dbh 工具](dbh.md)中为0x10C13。

### <a name="span-idsymopt-case-insensitivespanspan-idsymopt_case_insensitivespansymopt_case_insensitive"></a><span id="symopt-case-insensitive"></span><span id="SYMOPT_CASE_INSENSITIVE"></span>不 \_ 区分大小写 SYMOPT \_

此符号选项会使符号名称的所有搜索不区分大小写。

默认情况下，在所有调试器中启用此选项。 调试器运行后，可以分别使用 **. symopt + 0x1** 或 symopt-0x1 来打开或关闭该调试器。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 THIS->DBH 运行后，可以通过分别使用 symopt + 1 或 symopt-1 来打开或关闭该功能。

### <a name="span-idsymopt-undnamespanspan-idsymopt_undnamespansymopt_undname"></a><span id="symopt-undname"></span><span id="SYMOPT_UNDNAME"></span>SYMOPT \_ UNDNAME

此符号选项将导致公共符号名称在显示时被修饰，并导致搜索符号名称以忽略符号修饰。 不管此选项是否处于活动状态，都不会修饰私有符号名称。 有关符号名称修饰的信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

默认情况下，在所有调试器中启用此选项。 调试器运行后，可以分别使用 **. symopt + 0x2** 或. symopt-0x2 来打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 如果使用了-d 命令行选项，则该选项处于关闭状态。 THIS->DBH 运行后，可以通过分别使用 symopt + 2 或 symopt-2 来打开或关闭该功能。

### <a name="span-idsymopt-deferred-loadsspanspan-idsymopt_deferred_loadsspansymopt_deferred_loads"></a><span id="symopt-deferred-loads"></span><span id="SYMOPT_DEFERRED_LOADS"></span>SYMOPT \_ 延迟 \_ 加载

此符号选项称为 *延迟符号加载* 或 *延迟符号加载*。 处于活动状态时，在加载目标模块时，实际上不会加载符号。 而是在需要时由调试器加载符号。 有关详细信息，请参阅 [延迟符号加载](deferred-symbol-loading.md) 。

默认情况下，在所有调试器中启用此选项。 在 CDB 和 KD 中，-s 命令行选项将关闭此选项。 还可以通过使用[tools.ini](configuring-tools-ini.md)文件中的**LAZYLOAD**变量在 CDB 中关闭它。 调试器运行后，可以使用 **. symopt + 0x4** 或. symopt-0x4 来打开或关闭此选项。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以通过分别使用 symopt + 4 或 symopt-4 来打开或关闭该功能。

### <a name="span-idsymopt-no-cppspanspan-idsymopt_no_cppspansymopt_no_cpp"></a><span id="symopt-no-cpp"></span><span id="SYMOPT_NO_CPP"></span>SYMOPT \_ 无 \_ CPP

此符号选项用于关闭 c + + 转换。 设置此符号选项后，所有符号中将替换为 **：：** **\_\_** 。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-snc 命令行选项激活它。 调试器运行后，可以分别使用 **. symopt + 0x8** 或. symopt-0x8 来打开或关闭该调试器。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以分别使用 symopt + 8 或 symopt-8 来打开或关闭该功能。

### <a name="span-idsymopt-load-linesspanspan-idsymopt_load_linesspansymopt_load_lines"></a><span id="symopt-load-lines"></span><span id="SYMOPT_LOAD_LINES"></span>SYMOPT \_ 加载 \_ 线条

此符号选项允许从源文件中读取行号信息。 此选项必须为 on，源调试才能正常工作。

在 KD 和 CDB 中，此选项在默认情况下是关闭的;在 WinDbg 中，默认情况下此选项处于启用状态。 在 CDB 和 KD 中，-line 命令行选项将启用此选项。 调试器运行后，可以分别使用 **. symopt + 0x10** 或 symopt-0x10 来打开或关闭它。 还可以通过使用 [** (切换源代码行支持) **](-lines--toggle-source-line-support-.md) 命令来打开和关闭它。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 THIS->DBH 运行后，可以使用 symopt + 10 或 symopt-10 分别打开或关闭该功能。

### <a name="span-idsymopt-omap-find-nearestspanspan-idsymopt_omap_find_nearestspansymopt_omap_find_nearest"></a><span id="symopt-omap-find-nearest"></span><span id="SYMOPT_OMAP_FIND_NEAREST"></span>SYMOPT \_ OMAP \_ 查找 \_ 最近

如果代码已经过优化，且预期位置没有符号，则此选项将导致改用最近的符号。

默认情况下，在所有调试器中启用此选项。 调试器运行后，可以使用 **. symopt + 0x20** 或 symopt-0x20 来打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 THIS->DBH 运行后，可以分别使用 symopt + 20 或 symopt-20 打开或关闭该功能。

### <a name="span-idsymopt-load-anythingspanspan-idsymopt_load_anythingspansymopt_load_anything"></a><span id="symopt-load-anything"></span><span id="SYMOPT_LOAD_ANYTHING"></span>SYMOPT \_ 加载 \_ 任何内容

当符号处理程序尝试匹配符号时，此符号选项可减少符号处理程序的 pickiness。

默认情况下，此选项在所有调试器中处于关闭状态。 调试器运行后，可以使用 **. symopt + 0x40** 或 symopt-0x40 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 40 或 symopt-40 分别打开或关闭该功能。

### <a name="span-idsymopt-ignore-cvrecspanspan-idsymopt_ignore_cvrecspansymopt_ignore_cvrec"></a><span id="symopt-ignore-cvrec"></span><span id="SYMOPT_IGNORE_CVREC"></span>SYMOPT \_ 忽略 \_ CVREC

在搜索符号时，此符号选项导致符号处理程序忽略加载的图像标头中的 CV 记录。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-sicv 命令行选项激活它。 调试器运行后，可以分别使用 **. symopt + 0x80** 或 symopt-0x80 来打开或关闭该调试器。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 80 或 symopt-80 分别打开或关闭该功能。

### <a name="span-idsymopt-no-unqualified-loadsspanspan-idsymopt_no_unqualified_loadsspansymopt_no_unqualified_loads"></a><span id="symopt-no-unqualified-loads"></span><span id="SYMOPT_NO_UNQUALIFIED_LOADS"></span>SYMOPT \_ 无未 \_ 限定的 \_ 负载

此符号选项禁用符号处理程序的自动加载模块。 如果设置了此选项，并且调试器尝试匹配符号，则它将只搜索已加载的模块。

此选项可用于防范符号名称不键入的情况。 通常，键入错误的符号将导致调试器在搜索所有卸载的符号文件时暂停。 如果此选项处于活动状态，则在加载的模块中找不到错误键入的符号，然后搜索将终止。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-snul 命令行选项激活它。 调试器运行后，可以使用 **. symopt + 0x100** 或 symopt-0x100 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 100 或 symopt-100 分别打开或关闭该功能。

### <a name="span-idsymopt-fail-critical-errorsspanspan-idsymopt_fail_critical_errorsspansymopt_fail_critical_errors"></a><span id="symopt-fail-critical-errors"></span><span id="SYMOPT_FAIL_CRITICAL_ERRORS"></span>SYMOPT \_ 失败 \_ 严重 \_ 错误

此符号选项导致禁止显示文件访问错误对话框。

如果此选项为 off，则在符号加载过程中遇到的文件访问错误（如 "驱动器未就绪"）将导致显示对话框。 如果启用此选项，则会取消这些框，并且所有访问错误都将收到 "失败" 响应。

默认情况下，在所有调试器中启用此选项。 可以使用-sdce 命令行选项将其停用。 调试器运行后，可以使用 **. symopt + 0x200** 或 symopt-0x200 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 200 或 symopt-200 分别打开或关闭该功能。

### <a name="span-idsymopt-exact-symbolsspanspan-idsymopt_exact_symbolsspansymopt_exact_symbols"></a><span id="symopt-exact-symbols"></span><span id="SYMOPT_EXACT_SYMBOLS"></span>SYMOPT \_ 精确 \_ 符号

此符号选项使调试器对所有符号文件执行严格的计算。

如果选择此选项，即使符号文件与符号处理程序的预期之间的少许差异，也会导致忽略符号。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-ses 命令行选项激活它。 调试器运行后，可以使用 **. symopt + 0x400** 或 symopt-0x400 分别打开或关闭它。

-Failinc 命令行选项还会打开 SYMOPT 的 \_ 确切 \_ 符号。 此外，如果您正在调试用户模式小型转储或内核模式小型转储，则-failinc 将阻止调试器加载其图像无法映射的任何模块。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 THIS->DBH 运行后，可以使用 symopt + 400 或 symopt-400 分别打开或关闭该功能。

### <a name="span-idsymopt-allow-absolute-symbolsspanspan-idsymopt_allow_absolute_symbolsspansymopt_allow_absolute_symbols"></a><span id="symopt-allow-absolute-symbols"></span><span id="SYMOPT_ALLOW_ABSOLUTE_SYMBOLS"></span>SYMOPT \_ 允许 \_ 绝对 \_ 符号

此符号选项允许 Dbghelp.dll 读取存储在内存中的绝对地址的符号。 绝大多数情况下都不需要此选项。

默认情况下，此选项在所有调试器中处于关闭状态。 调试器运行后，可以使用 **. symopt + 0x800** 或 symopt-0x800 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 THIS->DBH 运行后，可以使用 symopt + 800 或 symopt-800 分别打开或关闭该功能。

### <a name="span-idsymopt-ignore-nt-sympathspanspan-idsymopt_ignore_nt_sympathspansymopt_ignore_nt_sympath"></a><span id="symopt-ignore-nt-sympath"></span><span id="SYMOPT_IGNORE_NT_SYMPATH"></span>SYMOPT \_ 忽略 \_ NT \_ SYMPATH

此符号选项使调试器忽略符号路径和可执行映像路径的环境变量设置。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-问题命令行选项激活它。 但是，在调试器运行后，不能对其进行控制 **。 symopt** ，因为只在启动时读取环境变量。

默认情况下，此选项在 THIS->DBH 中处于关闭状态，在所有情况下，THIS->DBH 将忽略此选项。

### <a name="span-idsymopt-publics-onlyspanspan-idsymopt_publics_onlyspansymopt_publics_only"></a><span id="symopt-publics-only"></span><span id="SYMOPT_PUBLICS_ONLY"></span>\_ \_ 仅限 SYMOPT PUBLICS

此符号选项导致 Dbghelp.dll 忽略 private 符号数据，并仅搜索公共符号表中的符号信息。 这会在添加对这些类型的支持之前模拟 Dbghelp.dll 的行为。 请参阅 [公共和私有符号](public-and-private-symbols.md)。

默认情况下，此选项在所有调试器中处于关闭状态。 调试器运行后，可以使用 **. symopt + 0x4000** 或 symopt-0x4000 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 如果使用了-d 命令行选项，则会将其打开。 THIS->DBH 运行后，可以使用 symopt + 4000 或 symopt-4000 分别打开或关闭该功能。

### <a name="span-idsymopt-no-publicsspanspan-idsymopt_no_publicsspansymopt_no_publics"></a><span id="symopt-no-publics"></span><span id="SYMOPT_NO_PUBLICS"></span>SYMOPT \_ NO \_ PUBLICS

此符号选项可防止 Dbghelp.dll 搜索公共符号表。 这会使符号枚举和符号搜索速度快得多。 如果仅关注搜索速度，SYMOPT \_ 自动 \_ PUBLICS 选项通常优于此选项。 有关公共符号表的信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

默认情况下，此选项在所有调试器中处于关闭状态。 调试器运行后，可以使用 **. symopt + 0x8000** 或. symopt-0x8000 来打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 8000 或 symopt-8000 分别打开或关闭该功能。

### <a name="span-idsymopt-auto-publicsspanspan-idsymopt-auto-publicsspansymopt_auto_publics"></a><span id="symopt-auto-publics"></span><span id="SYMOPT-AUTO-PUBLICS"></span>SYMOPT \_ 自动 \_ PUBLICS

此符号选项会使 Dbghelp.dll 仅搜索 .pdb 文件中的公共符号表，作为最后的手段。 如果在搜索私有符号数据时找到任何匹配项，则不会搜索公共符号。 这可提高符号搜索速度。

默认情况下，在所有调试器中启用此选项。 可以使用-sup 命令行选项将其停用。 调试器运行后，可以使用 **. symopt + 0x10000** 或 symopt-0x10000 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于启用状态。 如果使用了-d 命令行选项，则该选项处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 10000 或 symopt-10000 分别打开或关闭该功能。

### <a name="span-idsymopt-no-image-searchspanspan-idsymopt-no-image-searchspansymopt_no_image_search"></a><span id="symopt-no-image-search"></span><span id="SYMOPT-NO-IMAGE-SEARCH"></span>SYMOPT \_ 无 \_ 图像 \_ 搜索

在加载符号时，此符号选项可防止 Dbghelp.dll 在磁盘上搜索图像的副本。

默认情况下，在所有调试器中启用此选项。 调试器运行后，可以使用 **. symopt + 0x20000** 或 symopt-0x20000 分别打开或关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 20000 或 symopt-20000 分别打开或关闭该功能。

### <a name="span-idsymopt-securespanspan-idsymopt_securespansymopt_secure"></a><span id="symopt-secure"></span><span id="SYMOPT_SECURE"></span>SYMOPT \_ 安全

仅 (内核模式) 此符号选项指示 [安全模式](secure-mode.md) 是否处于活动状态。

默认情况下，所有调试器中的安全模式均为关闭状态。 可以使用-secure 命令行选项激活它。 如果调试器正在运行，处于休眠模式，并且尚未建立任何调试服务器，则可以通过使用 **. symopt + 0x40000** 或 [**安全 (激活安全模式) **](-secure--activate-secure-mode-.md)启用安全模式。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 40000 或 symopt-40000 分别打开或关闭该功能。

一旦激活，安全模式将无法关闭。

### <a name="span-idsymopt-no-promptsspanspan-idsymopt_no_promptsspansymopt_no_prompts"></a><span id="symopt-no-prompts"></span><span id="SYMOPT_NO_PROMPTS"></span>SYMOPT \_ 无 \_ 提示

此符号选项将取消代理服务器的身份验证对话框。 这可能会导致 SymSrv 无法访问 internet 上的符号存储。

有关详细信息，请参阅 [防火墙和代理服务器](firewalls-and-proxy-servers.md)。

在 KD 和 CDB 中，此选项在默认情况下是打开的;在 WinDbg 中，此选项在默认情况下处于关闭状态。 调试器运行后，可以使用 **. symopt + 0x80000** 或 symopt-0x80000 分别打开或关闭该调试器，然后 [** (再) **](-reload--reload-module-.md) 命令。 此外，还可以使用 [**！符号提示符 off**](-sym.md) 和 **！符号提示** 扩展命令，然后再执行 **. reload.sql (reload.sql Module) ** 命令来打开和关闭它。

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 THIS->DBH 运行后，可以使用 symopt + 80000 或 symopt-80000 分别打开或关闭该功能。

### <span id="symopt-disable-fast-symbols"></span>

### <span id="symopt_disable_symsrv_timeout"></span>

### <a name="span-idsymopt-debugspan-symopt_debug"></a><span id="symopt-debug"></span>-SYMOPT \_ 调试

此符号选项用于打开 *干扰符号加载*。 这会指示调试器显示有关其符号搜索的信息。

每个符号文件的名称将在加载时显示。 如果调试器无法加载符号文件，它将显示一条错误消息。 .Pdb 文件的错误消息将显示为文本。 Dbg 文件的错误消息将采用错误代码的形式;winerror.h 文件中对这些代码进行了说明。

如果加载的映像文件只是为了恢复符号标头信息，则也将显示该文件。

默认情况下，此选项在所有调试器中处于关闭状态。 可以使用-n 命令行选项激活它。 调试器运行后，可以分别使用 **. symopt + 0x80000000** 或 symopt-0x80000000 来打开或关闭该调试器。 还可以通过使用 [**！符号干扰**](-sym.md) 和 **！符号 quiet** extension 命令来打开和关闭它。

**注意**   不应将此选项与干扰*源*加载相混淆--由[**Srcnoisy (干扰源加载) **](-srcnoisy--noisy-source-loading-.md)命令。

 

默认情况下，此选项在 THIS->DBH 中处于关闭状态。 可以使用-n 命令行选项激活它。 THIS->DBH 运行后，可以使用 symopt + 80000000 或 symopt-80000000 分别打开或关闭该功能。 还可以使用详细的 on 和 verbose off 命令来打开和关闭它。

 

 





