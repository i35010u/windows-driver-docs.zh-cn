---
title: 调试 WinLogon
description: 调试 WinLogon
ms.assetid: c30e6b83-685a-4e4e-88bf-1e05776ac87a
keywords:
- 调试 WinLogon （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef49034e95e55e3f1a8aa55c69a8172759eb7a47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562377"
---
# <a name="debug-winlogon"></a>调试 WinLogon


## <span id="ddk_debug_winlogon_dtools"></span><span id="DDK_DEBUG_WINLOGON_DTOOLS"></span>


**调试 WinLogon**标志调试 WinLogon 服务。

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
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

NTSD 调试 Winlogon (通过使用命令**ntsd-d-g-x**)，但控件将重定向到内核调试程序。

NTSD 的详细信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[调试初始命令](debug-initial-command.md)，[启用调试的 Win32 子系统](enable-debugging-of-win32-subsystem.md)

 

 





