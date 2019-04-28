---
title: 调试初始命令
description: 调试初始命令
ms.assetid: 0af0b53d-455f-4cdb-b956-9d7e49601733
keywords:
- 调试初始命令 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: db307765b1432f3d435951c59b0f444c018a6e26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351191"
---
# <a name="debug-initial-command"></a>调试初始命令


## <span id="ddk_debug_initial_command_dtools"></span><span id="DDK_DEBUG_INITIAL_COMMAND_DTOOLS"></span>


**调试初始命令**标志调试客户端服务器运行时子系统 (CSRSS) 和 WinLogon 进程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>dic</p></td>
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
<td align="left"><p>整个系统的注册表项，内核标志</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

NTSD 对进程进行调试 (使用命令**ntsd-d**)，但控件将重定向到内核调试程序。

NTSD 的详细信息，请参阅[调试使用 CDB 和 NTSD](debugging-using-cdb-and-ntsd.md)。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用调试的 Win32 子系统](enable-debugging-of-win32-subsystem.md)

 

 





