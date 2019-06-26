---
title: DEFINE_DEVPROPKEY
description: 在 Windows Vista 和更高版本的 Windows，DEFINE_DEVPROPKEY 宏创建 DEVPROPKEY 结构，它表示一个统一的设备属性模型中的设备属性键。
ms.assetid: 9723241d-939e-40b4-8f06-83c99b31c02e
keywords:
- DEFINE_DEVPROPKEY 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEFINE_DEVPROPKEY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3de67065600fc6f9d2f143fc75d4a3aebd126f56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360837"
---
# <a name="definedevpropkey"></a>DEFINE_DEVPROPKEY


在 Windows Vista 和更高版本的 Windows，DEFINE_DEVPROPKEY 宏创建 DEVPROPKEY 结构，它表示中的设备属性键[统一的设备属性模型](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)。

``` syntax
#ifdef INITGUID
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY DECLSPEC_SELECTANY name = { { l, w1, w2, { b1, b2,  b3,  b4,  b5,  b6,  b7,  b8 } }, pid }
#else
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY name
#endif // INITGUID
```

## <a name="members"></a>成员


<a href="" id="name"></a>*name*  
表示设备属性键 DEVPROPKEY 结构的名称。

<a href="" id="l"></a>*l*  
无符号 long 类型的值类型的变量，用于提供的值**data1** DEVPROPKEY 结构的 fmtid 成员的成员。

<a href="" id="w1"></a>*w1*  
提供的值的无符号的短类型变量**data2**的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="w2"></a>*w2*  
提供的值的无符号的短类型变量**data3**的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b1"></a>*b1*  
字节类型，用于提供的值的变量**data4\[0\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b2"></a>*b2*  
字节类型，用于提供的值的变量**data4\[1\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b3"></a>*b3*  
字节类型，用于提供的值的变量**data4\[2\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b4"></a>*b4*  
字节类型，用于提供的值的变量**data4\[3\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b5"></a>*b5*  
字节类型，用于提供的值的变量**data4\[4\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b6"></a>*b6*  
字节类型，用于提供的值的变量**data4\[5\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b7"></a>*b7*  
字节类型，用于提供的值的变量**data4\[6\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="b8"></a>*b8*  
字节类型，用于提供的值的变量**data4\[7\]** 的成员**fmtid** DEVPROPKEY 结构中的成员。

<a href="" id="pid"></a>*pid*  
DEVPROPID 类型，用于提供的值的变量**pid** DEVPROPKEY 结构成员 （属性标识符）。 属性标识符必须是大于或等于 2。

<a name="remarks"></a>备注
-------

DEFINE_DEVPROPKEY 结构属于[统一的设备属性模型](https://docs.microsoft.com/windows-hardware/drivers/install/unified-device-property-model--windows-vista-and-later-)。

DEFINE_DEVPROPKEY 宏可以用于创建[ **DEVPROPKEY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)结构，它表示自定义设备属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h （包括 Devpropdef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROPKEY**](https://docs.microsoft.com/windows-hardware/drivers/install/devpropkey)

 

 






