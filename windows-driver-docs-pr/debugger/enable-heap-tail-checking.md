---
title: 启用堆尾部检查
description: 启用堆尾部检查
keywords:
- " (全局标志启用堆结尾检查) "
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d165a66fb639cc86160d39ce62d93d7d772d91b3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805737"
---
# <a name="enable-heap-tail-checking"></a>启用堆尾部检查


## <span id="ddk_enable_heap_tail_checking_dtools"></span><span id="DDK_ENABLE_HEAP_TAIL_CHECKING_DTOOLS"></span>


当释放堆时， **启用堆结尾检查** 标记将检查缓冲区溢出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>htc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAIL_CHECK</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

此标志将短模式添加到每个分配的末尾。 Windows 堆管理器会在释放块时检测模式，如果修改块，堆管理器会中断调试器。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆免费检查](enable-heap-free-checking.md)， [启用堆参数检查](enable-heap-parameter-checking.md)

 

 





