---
title: 调试初始命令
description: 调试初始命令
keywords:
- " (全局标志调试初始命令) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d24e61d98a88a3d7b4e6fa6ed78f39611795eec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817883"
---
# <a name="debug-initial-command"></a>调试初始命令


## <span id="ddk_debug_initial_command_dtools"></span><span id="DDK_DEBUG_INITIAL_COMMAND_DTOOLS"></span>


**Debug 初始命令** 标志用于调试客户端服务器运行时子系统 (CSRSS) 和 WinLogon 进程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>.dic</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x4</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围内的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

NTSD 使用命令 **ntsd**)  (调试进程，但会将控件重定向到内核调试器。

有关 NTSD 的详细信息，请参阅 [使用 CDB 和 NTSD 进行调试](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用 Win32 子系统调试](enable-debugging-of-win32-subsystem.md)

 

 





