---
title: 调试 \_ 过程 \_ XXX
description: 处理选项是控制调试器引擎如何处理 modeprocesses 的位集。 其中一些处理选项是全局的;其他特定于进程。
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_PROCESS_DETACH_ON_EXIT
- DEBUG_PROCESS_ONLY_THIS_PROCESS
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 18bd4c053e30b17f5b1e061ea616a1ad6eb4c1ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828245"
---
# <a name="debug_process_xxx"></a>调试 \_ 过程 \_ XXX


处理选项是控制 [调试器引擎](./introduction.md#debugger-engine) 如何处理用户模式[进程](./controlling-threads-and-processes.md#processes)的位集。 其中一些处理选项是全局的;其他特定于进程。

处理选项仅适用于实时用户模式调试。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位标志</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_PROCESS_DETACH_ON_EXIT"></span><span id="debug_process_detach_on_exit"></span>
<strong>DEBUG_PROCESS_DETACH_ON_EXIT</strong></td>
<td align="left"><p>调试器退出时，调试器会自动将自身与目标进程分离。 这是全局设置。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_PROCESS_ONLY_THIS_PROCESS"></span><span id="debug_process_only_this_process"></span>
<strong>DEBUG_PROCESS_ONLY_THIS_PROCESS</strong></td>
<td align="left"><p>调试器将不会调试此进程创建的子进程。</p></td>
</tr>
</tbody>
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
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**.childdbg**](./-childdbg--debug-child-processes-.md)

 

