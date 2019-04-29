---
title: WDF_PTR_ADD_OFFSET_TYPE 宏
description: WDF_PTR_ADD_OFFSET_TYPE 宏将偏移量的值添加到一个地址，并返回生成的地址强制转换为指定的类型。
ms.assetid: b46d0bbe-8401-4c97-8327-fecd3af50eca
keywords:
- WDF_PTR_ADD_OFFSET_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72632a005c9d2a2324d5c45977f6fef7a62f526c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366472"
---
# <a name="wdfptraddoffsettype-macro"></a>WDF_PTR_ADD_OFFSET_TYPE 宏


**WDF_PTR_ADD_OFFSET_TYPE**宏将偏移量的值添加到一个地址，并返回生成的地址强制转换为指定的类型。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
_type WDF_PTR_ADD_OFFSET_TYPE(
    _ptr,
    _offset,
    _type
);
```

<a name="parameters"></a>Parameters
----------

*_ptr*   
指定的地址。

*_offset*   
以字节为单位指定偏移量的值。

*_type*   
指定要返回的数据类型。

<a name="return-value"></a>返回值
------------

返回一个指向生成的地址。 选择中的返回值的数据类型*类型 （_t)* 宏的参数。

<a name="remarks"></a>备注
-------

定义宏，如下所示：

```ManagedCPlusPlus
#define WDF_PTR_ADD_OFFSET_TYPE(_ptr, _offset, _type) \
    ((_type) (((PUCHAR) (_ptr)) + (_offset)))
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfcore.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

 

 






