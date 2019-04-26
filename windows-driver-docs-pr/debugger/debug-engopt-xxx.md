---
title: DEBUG\_ENGOPT\_XXX
description: 调试\_ENGOPT\_XXX 常量是全局选项来影响调试器引擎的行为。
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ENGOPT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 857b755c3a6291067096e381d16e093bbbff2b66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330713"
---
# <a name="debugengoptxxx"></a>DEBUG\_ENGOPT\_XXX

以下全局选项会影响调试器引擎的行为。
<table>
<tr>
<th>Constant</th>
<th>描述</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_DBGHELP_VERSION"></a><a id="debug_engopt_ignore_dbghelp_version"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_DBGHELP_VERSION</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>如果 DbgHelp DLL 版本与调试器引擎的版本不匹配，则调试器引擎生成而不是错误的警告。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_EXTENSION_VERSIONS"></a><a id="debug_engopt_ignore_extension_versions"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_EXTENSION_VERSIONS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>禁用版本检查的扩展。  这会禁止 CheckVersion 调试器引擎的调用。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_ALLOW_NETWORK_PATHS"></a><a id="debug_engopt_allow_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_ALLOW_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>网络共享可用于加载符号和扩展。 此选项可阻止引擎调试某些系统进程时不允许网络路径，因此应谨慎使用。</p>
<p>如果设置 DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS，不能设置此选项。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS"></a><a id="debug_engopt_disallow_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>网络共享不能用于加载符号和扩展。 引擎将尝试调试某些系统进程时设置此选项。</p>
<p>如果设置 DEBUG_ENGOPT_ALLOW_NETWORK_PATHS，不能设置此选项。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_NETWORK_PATHS"></a><a id="debug_engopt_network_paths"></a><dl>
<dt><b>DEBUG_ENGOPT_NETWORK_PATHS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>DEBUG_ENGOPT_ALLOW_NETWORK_PATHS 和 DEBUG_ENGOPT_DISALLOW_NETWORK_PATHS 的按位 OR。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_IGNORE_LOADER_EXCEPTIONS"></a><a id="debug_engopt_ignore_loader_exceptions"></a><dl>
<dt><b>DEBUG_ENGOPT_IGNORE_LOADER_EXCEPTIONS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>忽略生成的某些较旧版本的 Windows 中的加载程序的预期的最可能异常。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_INITIAL_BREAK"></a><a id="debug_engopt_initial_break"></a><dl>
<dt><b>DEBUG_ENGOPT_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>在目标的初始事件在调试器中中断。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_INITIAL_MODULE_BREAK"></a><a id="debug_engopt_initial_module_break"></a><dl>
<dt><b>DEBUG_ENGOPT_INITIAL_MODULE_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当目标加载其第一个模块时中断调试器。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_FINAL_BREAK"></a><a id="debug_engopt_final_break"></a><dl>
<dt><b>DEBUG_ENGOPT_FINAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>在目标的最后一个事件在调试器中中断。 在实时用户模式目标，这是在进程退出时。 在内核模式下，它具有不起作用。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_NO_EXECUTE_REPEAT"></a><a id="debug_engopt_no_execute_repeat.md"></a><dl>
<dt><b>DEBUG_ENGOPT_NO_EXECUTE_REPEAT</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>当给定空命令，调试器引擎不重复最后一个命令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_FAIL_INCOMPLETE_INFORMATION"></a><a id="debug_engopt_fail_incomplete_information.md"></a><dl>
<dt><b>DEBUG_ENGOPT_FAIL_INCOMPLETE_INFORMATION</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>防止调试器加载的模块不能映射其映像。</p>
<p>调试器会尝试在不包含图像的小型转储调试时加载图像。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_ALLOW_READ_ONLY_BREAKPOINTS"></a><a id="debug_engopt_allow_read_only_breakpoints"></a><dl>
<dt><b>DEBUG_ENGOPT_ALLOW_READ_ONLY_BREAKPOINTS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>允许调试器引擎来操作以允许在内存的只读部分中设置软件断点在目标上的页保护。</p>
<p>设置软件断点时，该引擎以透明方式更改目标的内存要插入的中断指令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_SYNCHRONIZE_BREAKPOINTS"></a><a id="debug_engopt_synchronize_breakpoints"></a><dl>
<dt><b>DEBUG_ENGOPT_SYNCHRONIZE_BREAKPOINTS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>在实时用户模式下调试中，则引擎将执行额外的工作时插入和删除断点，以确保在目标中的所有线程在所有时间都都一致断点状态。</p>
<p>当多个线程可以使用为其设置断点的代码时，此选项非常有用。 但是，它可能会带来的死锁的可能性。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_SHELL_COMMANDS"></a><a id="debug_engopt_disallow_shell_commands"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_SHELL_COMMANDS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>不允许通过调试器执行 shell 命令。</p>
<p>设置此选项后，它不能取消设置。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_KD_QUIET_MODE"></a><a id="debug-engopt-kd-quiet-mode.md"></a><dl>
<dt><b>DEBUG_ENGOPT_KD_QUIET_MODE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>启用无人参与模式。 有关详细信息，请参阅<a href="sq--set-quiet-mode-.md"> <b>sq （设置安静模式下）</b></a>。 </p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_MANAGED_SUPPORT"></a><a id="debug_engopt_disable_managed_support"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_MANAGED_SUPPORT</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>禁用调试器引擎支持托管代码。 如果支持中的托管的代码已使用，此选项不起作用。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_MODULE_SYMBOL_LOAD"></a><a id="debug_engopt_disable_module_symbol_load"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_MODULE_SYMBOL_LOAD</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>调试器不会加载用于设置此标志时加载的模块的符号。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLE_EXECUTION_COMMANDS"></a><a id="debug_engopt_disable_execution_commands"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLE_EXECUTION_COMMANDS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>可以防止任何会导致目标开始执行的命令。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISALLOW_IMAGE_FILE_MAPPING"></a><a id="debug_engopt_disallow_image_file_mapping"></a><dl>
<dt><b>DEBUG_ENGOPT_DISALLOW_IMAGE_FILE_MAPPING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>不允许从磁盘图像文件的映射。 例如，此选项不允许在调试小型转储文件的过程中内存内容的图像映射。
此选项不会影响现有的映射;它会影响仅后续尝试将图像文件映射。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_PREFER_DML"></a><a id="debug_engopt_prefer_dml"></a><dl>
<dt><b>DEBUG_ENGOPT_PREFER_DML</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>默认情况下，调试器运行命令和操作的 DML 增强版本。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ENGOPT_DISABLESQM"></a><a id="debug_engopt_disablesqm"></a><dl>
<dt><b>DEBUG_ENGOPT_DISABLESQM</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>禁用软件质量指标 (SQM) 数据上传。</p>
</td>
</tr>
</table>


<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

 
