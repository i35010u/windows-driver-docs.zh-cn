---
title: 调试 \_ 附加 \_ XXX
description: '\_ \_ 本主题中所述的 DEBUG 附加*XXX*位标志控制调试器引擎如何附加到用户模式进程。'
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ATTACH_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: f696e7df10e3b8de10c31bae468d4e23e5bc44ef
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213489"
---
# <a name="debug_attach_xxx"></a>调试 \_ 附加 \_ XXX

\_ \_ 本主题中所述的 DEBUG 附加*XXX*位标志控制调试器引擎如何附加到用户模式进程。 对于附加到内核目标时使用的 DEBUG_ATTACH_XXX 选项，请参见 [IDebugClient：： AttachKernel 方法](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient-attachkernel)。

可能的值包括以下各项。

<table>
<tr>
<th>返回的常量</th>
<th>说明</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE"></a><a id="debug_attach_noninvasive"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加到目标 noninvasively。  有关 noninvasive 调试的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-" data-raw-source="[Noninvasive Debugging (User Mode)](./noninvasive-debugging--user-mode-.md)">Noninvasive 调试 (用户模式) </a>。</p>
<p>如果设置了此标志，则不得设置标志 DEBUG_ATTACH_EXISTING、DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK 和 DEBUG_ATTACH_INVASIVE_RESUME_PROCESS。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_EXISTING"></a><a id="debug_attach_existing"></a><dl>
<dt><b>DEBUG_ATTACH_EXISTING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>重新附加到调试器已附加到的应用程序 (可能被放弃) 。  有关重新附加到目标的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-" data-raw-source="[.attach (Attach to Process)](./-attach--attach-to-process-.md)">。附加 (附加到进程) </a>。</p>
<p>如果设置了此标志，则不得设置其他 DEBUG_ATTACH_<i>XXX</i> 标志。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND"></a><a id="debug_attach_noninvasive_no_suspend"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加 noninvasively 时，请勿挂起目标的线程。</p>
<p>如果设置了此标志，则还必须设置标志 DEBUG_ATTACH_NONINVASIVE。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK"></a><a id="debug_attach_invasive_no_initial_break"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加到目标时，请勿请求初始中断。</p>
<p>如果设置了此标志，则不得设置标志 DEBUG_ATTACH_NONINVASIVE 和 DEBUG_ATTACH_EXISTING。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_RESUME_PROCESS"></a><a id="debug_attach_invasive_resume_process"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_RESUME_PROCESS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加 invasively 时恢复目标的所有线程。</p>
<p>如果设置了此标志，则不得设置标志 DEBUG_ATTACH_NONINVASIVE 和 DEBUG_ATTACH_EXISTING。</p>
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
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

 

