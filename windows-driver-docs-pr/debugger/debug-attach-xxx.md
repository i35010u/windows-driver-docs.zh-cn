---
title: DEBUG\_ATTACH\_XXX
description: 调试\_附加\_*XXX*位标志在本主题中所述控制调试器引擎如何附加到用户模式进程。
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
ms.openlocfilehash: a7823934b3ea377d9a5a45d44748713d3ffa4683
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350382"
---
# <a name="debugattachxxx"></a>DEBUG\_ATTACH\_XXX

调试\_附加\_*XXX*位标志在本主题中所述控制调试器引擎如何附加到用户模式进程。 有关 DEBUG_ATTACH_XXX 选项时，使用附加到内核目标，请参阅[IDebugClient::AttachKernel 方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient-attachkernel)。

可能的值包括以下内容。

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
<p>将 noninvasively 附加到目标。  有关非侵入调试的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-" data-raw-source="[Noninvasive Debugging (User Mode)](https://docs.microsoft.com/windows-hardware/drivers/debugger/noninvasive-debugging--user-mode-)">非侵入调试 （用户模式）</a>。</p>
<p>如果设置此标志，则不能设置 DEBUG_ATTACH_EXISTING、 DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK 和 DEBUG_ATTACH_INVASIVE_RESUME_PROCESS 的标志。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_EXISTING"></a><a id="debug_attach_existing"></a><dl>
<dt><b>DEBUG_ATTACH_EXISTING</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>重新附加到应用程序到调试程序具有已附加 （和可能是放弃）。  有关重新附加到目标的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-" data-raw-source="[.attach (Attach to Process)](https://docs.microsoft.com/windows-hardware/drivers/debugger/-attach--attach-to-process-)">.attach （附加到进程）</a>。</p>
<p>如果此标志设置，那么其他 DEBUG_ATTACH_<i>XXX</i>标志不能设置。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND"></a><a id="debug_attach_noninvasive_no_suspend"></a><dl>
<dt><b>DEBUG_ATTACH_NONINVASIVE_NO_SUSPEND</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加 noninvasively 时不挂起目标线程。</p>
<p>如果设置此标志，然后将标志 DEBUG_ATTACH_NONINVASIVE 还必须进行设置。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK"></a><a id="debug_attach_invasive_no_initial_break"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_NO_INITIAL_BREAK</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加到目标时不请求初始被侵入的情形。</p>
<p>如果设置此标志，必须不设置 DEBUG_ATTACH_NONINVASIVE 和 DEBUG_ATTACH_EXISTING 的标志。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ATTACH_INVASIVE_RESUME_PROCESS"></a><a id="debug_attach_invasive_resume_process"></a><dl>
<dt><b>DEBUG_ATTACH_INVASIVE_RESUME_PROCESS</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>附加 invasively 时恢复所有目标的线程。</p>
<p>如果设置此标志，必须不设置 DEBUG_ATTACH_NONINVASIVE 和 DEBUG_ATTACH_EXISTING 的标志。</p>
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

 

 





