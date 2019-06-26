---
title: DEBUG\_PROCESS\_XXX
description: 处理选项，可控制调试器引擎如何处理用户 modeprocesses 有点设置。 其中某些进程选项是全局;其他人是特定于进程。
ms.assetid: 5b485ae2-6d97-4cfc-b2bf-ad8ddca268a8
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
ms.openlocfilehash: dd957c3e15efbc2a06f05374b5b43a05852a8f72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366979"
---
# <a name="debugprocessxxx"></a>DEBUG\_PROCESS\_XXX


处理选项有点设置该控件如何[调试器引擎](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)将用户模式[进程](https://docs.microsoft.com/windows-hardware/drivers/debugger/controlling-threads-and-processes#processes)。 其中某些进程选项是全局;其他人是特定于进程。

处理选项仅适用于实时用户模式下调试。

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
<td align="left"><p>调试器自动分离本身从目标进程时调试器将退出。 这是一种全局设置。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_PROCESS_ONLY_THIS_PROCESS"></span><span id="debug_process_only_this_process"></span>
<strong>DEBUG_PROCESS_ONLY_THIS_PROCESS</strong></td>
<td align="left"><p>调试器不会调试此进程创建的子进程。</p></td>
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
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h （包括 DbgEng.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[ **.childdbg**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-childdbg--debug-child-processes-)

 

 






