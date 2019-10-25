---
title: 调试\_附加\_XXX
description: DEBUG\_附加了本主题中介绍的\_*XXX*位标志控制调试器引擎如何附加到用户模式进程。
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
ms.openlocfilehash: de54d41b7b4fcd9f0616097ec3b088a192f4fcb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837796"
---
# <a name="debug_attach_xxx"></a>调试\_附加\_XXX

DEBUG\_附加了本主题中介绍的\_*XXX*位标志控制调试器引擎如何附加到用户模式进程。 对于附加到内核目标时使用的 DEBUG_ATTACH_XXX 选项，请参阅[IDebugClient：： AttachKernel 方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient-attachkernel)。

可能的值包括以下各项。

<table>
<tr>
<th>Constant</th>
<th>描述</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE"></a><a id="debug_attach_noninvasive"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加到目标 noninvasively。  有关 noninvasive 调试的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-" data-raw-source="[Noninvasive Debugging (User Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-)">Noninvasive 调试（用户模式）</a>。</p>
<p>如果设置了此标志，则不得设置标志 DEBUG_ATTACH_EXISTING、DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK 和 DEBUG_ATTACH_INVASIVE_RESUME_PROCESS。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_EXISTING"></a><a id="debug_attach_existing"></a><dl>
<dt><b>DEBUG_ATTACH_EXISTING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>重新附加到调试器已附加的应用程序（可能已被放弃）。  有关重新附加到目标的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-" data-raw-source="[.attach (Attach to Process)](https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-)">。附加（附加到进程）</a>。</p>
<p>如果设置了此标志，则不得设置其他 DEBUG_ATTACH_<i>XXX</i>标志。</p>
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
<td align="left">DbgEng （包括 DbgEng）</td>
</tr>
</tbody>
</table>

 

 





