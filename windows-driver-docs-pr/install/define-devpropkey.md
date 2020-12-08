---
title: DEFINE_DEVPROPKEY
description: 在 Windows Vista 和更高版本的 Windows 中，DEFINE_DEVPROPKEY 宏会在统一设备属性模型中创建一个表示设备属性键的 DEVPROPKEY 结构。
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
ms.openlocfilehash: a60962c5fd1c2797596829425276108c608b42a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782907"
---
# <a name="define_devpropkey"></a>DEFINE_DEVPROPKEY


在 Windows Vista 和更高版本的 Windows 中，DEFINE_DEVPROPKEY 宏会在 [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md)中创建一个表示设备属性键的 DEVPROPKEY 结构。

``` syntax
#ifdef INITGUID
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY DECLSPEC_SELECTANY name = { { l, w1, w2, { b1, b2,  b3,  b4,  b5,  b6,  b7,  b8 } }, pid }
#else
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY name
#endif // INITGUID
```

## <a name="members"></a>成员


<a href="" id="name"></a>*路径名*  
表示设备属性键的 DEVPROPKEY 结构的名称。

<a href="" id="l"></a>*l*  
一个无符号的长类型变量，它提供 DEVPROPKEY 结构的 fmtid 成员的 **data1** 成员的值。

<a href="" id="w1"></a>*w1*  
一个无符号的 short 类型变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data2** 成员的值。

<a href="" id="w2"></a>*w2*  
一个无符号的 short 类型变量，该变量提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data3** 成员的值。

<a href="" id="b1"></a>*b1*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 0 \]** 成员的值。

<a href="" id="b2"></a>*b2*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 1 \]** 成员的值。

<a href="" id="b3"></a>*b3*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 2 \]** 成员的值。

<a href="" id="b4"></a>*b4*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 3 \]** 成员的值。

<a href="" id="b5"></a>*b5*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 4 \]** 成员的值。

<a href="" id="b6"></a>*b6*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 5 \]** 成员的值。

<a href="" id="b7"></a>*b7*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 6 \]** 成员的值。

<a href="" id="b8"></a>*b8*  
一个字节类型的变量，它提供 DEVPROPKEY 结构的 **fmtid** 成员的 **data4 \[ 7 \]** 成员的值。

<a href="" id="pid"></a>*p&id*  
DEVPROPID 类型的变量，该变量提供 DEVPROPKEY 结构的) 成员的 **pid** (属性标识符的值。 属性标识符必须大于或等于2。

<a name="remarks"></a>备注
-------

DEFINE_DEVPROPKEY 结构是 [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md)的一部分。

DEFINE_DEVPROPKEY 宏可用于创建表示自定义设备属性的 [**DEVPROPKEY**](./devpropkey.md) 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPROPKEY**](./devpropkey.md)

 

