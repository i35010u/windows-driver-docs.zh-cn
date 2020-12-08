---
title: 调试 WinLogon
description: 调试 WinLogon
keywords:
- '调试 WinLogon (全局标志) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23e230681971c1b4904553c4930365b428ff2f10
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788829"
---
# <a name="debug-winlogon"></a>调试 WinLogon


## <span id="ddk_debug_winlogon_dtools"></span><span id="DDK_DEBUG_WINLOGON_DTOOLS"></span>


**调试 winlogon 标志调试** winlogon 服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dwl</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x04000000</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND_EX</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

NTSD 使用命令 **ntsd-d-g-x**) 调试 Winlogon (，但会将控件重定向到内核调试器。

有关 NTSD 的详细信息，请参阅 [使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[调试初始命令](debug-initial-command.md)， [启用 Win32 子系统调试](enable-debugging-of-win32-subsystem.md)

 

 





