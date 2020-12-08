---
title: 异常时停止
description: 异常时停止
keywords:
- '发生异常时停止 (全局标志) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 773d9f7e62aa8313b90973904406b2e04894aabb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803599"
---
# <a name="stop-on-exception"></a>异常时停止


## <span id="ddk_stop_on_exception_dtools"></span><span id="DDK_STOP_ON_EXCEPTION_DTOOLS"></span>


每当发生内核模式异常时，" **异常时停止** " 标志将导致内核进入内核调试器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>soe</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_STOP_ON_EXCEPTION</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

Windows 将除状态端口断开) 之外的所有第一次机会异常 (传递到 \_ \_ 调试器，然后将其传递给本地异常处理程序。

 

 





