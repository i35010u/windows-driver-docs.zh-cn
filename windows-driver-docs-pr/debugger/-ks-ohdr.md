---
title: ks.ohdr
description: Ks.ohdr 扩展显示流对象的标题是内核的详细的信息。
ms.assetid: 0080565a-537d-44f4-9329-9ebe7fc926a1
keywords:
- ks.ohdr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.ohdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd0b4e8adee51a098eb9eab51fd96165b1cf151e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525045"
---
# <a name="ksohdr"></a>!ks.ohdr


**！ Ks.ohdr**扩展显示的流对象的标题是内核的详细信息。

```dbgcmd
!ks.ohdr Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *Object*   
此参数指定指向 KS 对象标头的指针。 如果*对象*不是有效的该命令将返回错误。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *级别*   
可选。 值是与用于相同[ **！ ks.dump**](-ks-dump.md)。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
可选。 值是与用于相同[ **！ ks.dump**](-ks-dump.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

**！ Ks.ohdr**命令的工作原理类似于[ **！ ks.objhdr** ](-ks-objhdr.md) ，因为它显示 KS 对象标头的详细信息。 不同之处在于，调用方提供 KS 对象标头，而不是关联的文件对象的地址直接寻址。

级别和标志 **！ ks.ohdr**中所述相同[ **！ ks.dump**](-ks-dump.md)。

如果你正在查询的数据不换出时，请考虑使用[ **！ ks.dump** ](-ks-dump.md)而不是 **！ ks.ohdr**。

 

 





