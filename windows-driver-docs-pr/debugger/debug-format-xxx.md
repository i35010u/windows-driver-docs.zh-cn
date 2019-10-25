---
title: '\_XXX 调试\_格式'
description: WriteDumpFile2 和 WriteDumpFileWide 使用 DEBUG_FORMAT_XXX 位标志来确定故障转储文件的格式，对于用户模式小型转储，还使用它们来确定要包含在文件中的信息。
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
ms.openlocfilehash: 60aa527199b5fe2b395200fdf2dd8b059e7794e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837793"
---
# <a name="debug_format_xxx"></a>\_XXX 调试\_格式

WriteDumpFile2 和 WriteDumpFileWide 使用 DEBUG_FORMAT_XXX 位标志来确定故障转储文件的格式，对于用户模式小型转储，还使用它们来确定要包含在文件中的信息。

以下位标志适用于所有故障转储文件。

<table>
<tr>
<th>Value</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_WRITE_CAB</p>
</td>
<td>
<p>将故障转储文件打包到 CAB 文件中。  提供的文件名或文件句柄用于 CAB 文件;崩溃转储首先在临时文件中创建，然后再移到 CAB 文件中。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_CAB_SECONDARY_FILES</p>
</td>
<td>
<p>
<dl>
<dt>在 CAB 文件中包含当前符号和映射的图像。</dt>
<dt>如果未设置 DEBUG_FORMAT_WRITE_CAB，则忽略此标志。</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_NO_OVERWRITE</p>
</td>
<td>
<p>不要覆盖现有文件。</p>
</td>
</tr>
</table>
<p> </p>
<p>对于用户模式小型转储，还可以包含以下位标志。</p>
<table>
<tr>
<th>Value</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY</p>
</td>
<td>
<p>添加完整内存数据。  将包括目标应用程序拥有的所有可访问的已提交页面。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_HANDLE_DATA</p>
</td>
<td>
<p>添加与目标应用程序关联的句柄的相关数据。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_UNLOADED_MODULES</p>
</td>
<td>
<p>添加卸载的模块信息。  此信息仅在 Windows Server 2003 和更高版本的 Windows 中可用。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY</p>
</td>
<td>
<p>添加间接内存。  包含堆栈或后备存储中的指针所引用的任何地址的小型内存区域。</p>
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
<p>将堆栈和后备存储中的所有内存均设置为零，这对于重新创建堆栈跟踪不起作用。  这样可以更高效地压缩小型转储，并通过删除不必要的信息来提高隐私性。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_PATHS</p>
</td>
<td>
<p>删除模块路径，仅保留模块名称。  这对于通过隐藏目录结构（可能包含用户的名称）来保护隐私非常有用。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FILTER_TRIAGE</p>
</td>
<td>
<p>此格式用于筛选出不是指向转储中捕获的其他数据的指针的任何数据。 标志可用于减少转储中存在的专用数据量，同时仍允许诊断故障。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA</p>
</td>
<td>
<p>添加进程环境块（PEB）和线程环境块（TEB）。  此标志可用于为线程和进程提供 Windows 系统信息。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</p>
</td>
<td>
<p>添加所有已提交的专用读写内存页。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_NO_OPTIONAL_DATA</p>
</td>
<td>
<p>
<dl>
<dt>防止在小型转储中包含隐私敏感数据。 目前，由于正在设置以下标志，此标志将从已添加的小型转储数据中排除：</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PROCESS_THREAD_DATA、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_INDIRECT_MEMORY、</dt>
<dt>DEBUG_FORMAT_USER_SMALL_PRIVATE_READ_WRITE_MEMORY</dt>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_FULL_MEMORY_INFO</p>
</td>
<td>
<p>添加所有基本内存信息。  这是<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual" data-raw-source="[IDebugDataSpaces2::QueryVirtual method](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces2-queryvirtual)">IDebugDataSpaces2：： QueryVirtual 方法</a>返回的信息。  包括所有内存的信息，而不只是有效的内存，这允许调试器从小型转储构造完整的虚拟内存布局。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_THREAD_INFO</p>
</td>
<td>
<p>添加其他线程信息，其中包括执行时间、开始时间、退出时间、开始地址和退出状态。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_FORMAT_USER_SMALL_CODE_SEGMENTS</p>
</td>
<td>
<p>添加包含可执行映像的所有代码段。</p>
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
<td align="left"><p>标头</p></td>
<td align="left">DbgEng （包括 DbgEng）</td>
</tr>
</tbody>
</table>
 





