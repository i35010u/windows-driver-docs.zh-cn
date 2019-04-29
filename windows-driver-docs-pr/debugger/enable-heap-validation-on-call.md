---
title: 启用调用时进行堆验证
description: 启用调用时进行堆验证
ms.assetid: 779871e0-f8b9-4eb5-9869-8df67586ffab
keywords:
- 启用堆验证的调用 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ef3612e2222a88ee5ac0939e06a287d7579879
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379144"
---
# <a name="enable-heap-validation-on-call"></a>启用调用时进行堆验证


## <span id="ddk_enable_heap_validation_on_call_dtools"></span><span id="DDK_ENABLE_HEAP_VALIDATION_ON_CALL_DTOOLS"></span>


**堆上启用验证调用**标志验证整个堆每次调用堆函数。

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
<td align="left"><p>整个系统的注册表项、 内核标志和图像文件注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

若要避免开销与此标志关联的最高，请使用**HeapValidate**函数而不是设置此标志，尤其是在关键衔接点，例如何时销毁堆。 但是，此标志可用于检测在池中随机损坏。

### <a name="span-idseealsospanspan-idseealsospansee-also"></a><span id="see_also"></span><span id="SEE_ALSO"></span>另请参阅

[启用堆参数检查](enable-heap-parameter-checking.md)

 

 





