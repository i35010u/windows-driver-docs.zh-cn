---
title: 启用堆尾部检查
description: 启用堆尾部检查
ms.assetid: d71b4567-55e7-49e6-a791-a292ad477c10
keywords:
- 启用堆结尾检查 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2dc92c023e19e1a0a7109b242274faad9f62395
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567222"
---
# <a name="enable-heap-tail-checking"></a>启用堆尾部检查


## <span id="ddk_enable_heap_tail_checking_dtools"></span><span id="DDK_ENABLE_HEAP_TAIL_CHECKING_DTOOLS"></span>


**启用堆结尾检查**标志时，将释放在堆缓冲区溢出检查。

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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

此标志将短模式添加到每个分配的末尾。 Windows 堆管理器检测到模式，当释放块，如果块已修改，堆管理器进入调试器。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆免费检查](enable-heap-free-checking.md)，[启用堆参数检查](enable-heap-parameter-checking.md)

 

 





