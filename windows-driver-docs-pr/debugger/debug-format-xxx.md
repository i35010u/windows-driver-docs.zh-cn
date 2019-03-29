---
title: 调试\_格式\_XXX
description: WriteDumpFile2 和 WriteDumpFileWide 使用 DEBUG_FORMAT_XXX 位标志来确定的崩溃转储文件，并且对于用户模式的小型转储，要在文件中包含的信息的格式。
ms.date: 08/20/2018
topic_type:
- apiref
api_name:
- DEBUG_FORMAT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 429a2f8164504b133bb7e02beb60fff5ff012413
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349694"
---
# <a name="debugformatxxx"></a>调试\_格式\_XXX

WriteDumpFile2 和 WriteDumpFileWide 使用 DEBUG_FORMAT_XXX 位标志来确定的崩溃转储文件，并且对于用户模式的小型转储，要在文件中包含的信息的格式。

以下位标志适用于所有的故障转储文件。

<table>
<tr>
<th>值</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_WRITE_CAB</p>
</td>
<td>
<p>打包到 CAB 文件中的故障转储文件。  提供的文件名称或文件句柄用于 CAB 文件中;故障转储是在首次创建临时文件之前要移到 CAB 文件。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_CAB_SECONDARY_FILES</p>
</td>
<td>
<p>
<dl>
<dt>在 CAB 文件中包含的当前符号和映射的映像。</dt>
<dt>如果 DEBUG_FORMAT_WRITE_CAB 未设置，则忽略此标志。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_NO_OVERWRITE</p>
</td>
<td>
<p>不会覆盖现有文件。</p>
</td>
</tr>
</table>
<p> </p>
<p>以下位标志也可以是包含用户模式的小型转储。</p>
<table>
<tr>
<th>ReplTest1</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY</p>
</td>
<td>
<p>添加完整的内存数据。  将包含在目标应用程序所拥有的所有可访问已提交的页面。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_HANDLE_DATA</p>
</td>
<td>
<p>添加有关目标应用程序与关联的句柄的数据。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_UNLOADED_MODULES</p>
</td>
<td>
<p>添加已卸载的模块的信息。  仅在 Windows Server 2003 和更高版本的 Windows 中提供了此信息。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY</p>
</td>
<td>
<p>添加间接内存。  包含环绕的堆栈或后备存储的指针引用的任何地址的内存小区域。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_DATA_SEGMENTS</p>
</td>
<td>
<p>添加可执行映像中的所有数据段。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_MEMORY</p>
</td>
<td>
<p>设置为零的所有内存在堆栈上并不是可用于重新创建的堆栈跟踪的后备存储区中。  这可以提高压缩的小型转储的效率，并通过删除不必要的信息来提高隐私。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_PATHS</p>
</td>
<td>
<p>删除模块路径，并保持仅模块名称。  这可用于通过隐藏的目录结构 （其中可能包含用户的名称） 来保护隐私。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_TRIAGE</p>
</td>
<td>
<p>此格式用于筛选出不是指向在转储捕获的其他数据的任何数据。 该标志可以用于减少的同时仍允许以进行诊断的崩溃转储中存在专用数据。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA</p>
</td>
<td>
<p>添加进程环境块 (PEB) 和线程环境块 (TEB)。  可以使用此标志为线程和进程提供 Windows 系统信息。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</p>
</td>
<td>
<p>添加所有已提交的读写的专用内存页面。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_NO_OPTIONAL_DATA</p>
</td>
<td>
<p>
<dl>
<dt>阻止隐私敏感的数据包含的小型转储中。目前，此标志会从正在设置的以下标志由于添加的小型转储数据中排除：</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA，</dt>
<dt>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY，</dt>
<dt>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY，</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY_INFO</p>
</td>
<td>
<p>添加基本的内存的所有信息。  这是返回的信息<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual" data-raw-source="[IDebugDataSpaces2::QueryVirtual method](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual)">IDebugDataSpaces2::QueryVirtual 方法</a>。  所有内存的信息不包括的不只是有效的内存，这使调试器能够重新构造完整的虚拟内存布局从小型转储。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_THREAD_INFO</p>
</td>
<td>
<p>添加其他线程的信息，其中包括执行时间、 开始时间、 退出时间、 起始地址，并退出状态。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_CODE_SEGMENTS</p>
</td>
<td>
<p>添加与可执行映像的所有代码段。</p>
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
 





