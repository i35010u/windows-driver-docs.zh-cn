---
title: 启用调用时进行堆验证
description: 启用调用时进行堆验证
keywords:
- '在调用 (全局标志时启用堆验证) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6ba31bd2db5739ff28f93d7a070a372365a1277
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826153"
---
# <a name="enable-heap-validation-on-call"></a>启用调用时进行堆验证


## <span id="ddk_enable_heap_validation_on_call_dtools"></span><span id="DDK_ENABLE_HEAP_VALIDATION_ON_CALL_DTOOLS"></span>


" **对调用启用堆验证** " 标志会在每次调用堆函数时验证整个堆。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>hvc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x80</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_ALL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>系统范围的注册表项、内核标志、映像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

若要避免与此标志关联的高开销，请使用 **HeapValidate** 函数而不是设置此标志，特别是在关键时刻（例如，在销毁堆时）。 但是，此标志对于检测池中的随机损坏很有用。

### <a name="span-idsee_alsospanspan-idsee_alsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆参数检查](enable-heap-parameter-checking.md)

 

 





