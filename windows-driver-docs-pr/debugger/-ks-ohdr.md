---
title: ks. ohdr
description: Ohdr 扩展显示内核流式处理对象标头的详细信息。
keywords:
- ohdr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.ohdr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 32db8d16ffcd53a107efc060afb11d2192f926bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804071"
---
# <a name="ksohdr"></a>!ks.ohdr


**Ohdr** 扩展显示内核流式处理对象标头的详细信息。

```dbgcmd
!ks.ohdr Object [Level] [Flags]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span>*对象*   
此参数指定指向 KS 对象标头的指针。 如果 *对象* 无效，则该命令将返回一个错误。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span>*级别*   
可选。 值与 [**！ ks**](-ks-dump.md)的值相同。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
可选。 值与 [**！ ks**](-ks-dump.md)的值相同。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

**Ohdr** 命令的工作方式类似于 [**！ objhdr**](-ks-objhdr.md) ，因为它显示了 ks 对象标头的详细信息。 不同之处在于调用方提供 KS 对象标头的直接地址，而不是关联的文件对象的地址。

**！ Ks** 的级别和标志与 [**！ ks**](-ks-dump.md)中描述的 ohdr 相同。

如果要查询的数据未分页，请考虑使用 [**！ ks**](-ks-dump.md) ，而不是 **！ ohdr**。

 

 





