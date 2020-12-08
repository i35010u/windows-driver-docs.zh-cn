---
title: WDF_PTR_ADD_OFFSET_TYPE 宏
description: WDF_PTR_ADD_OFFSET_TYPE 宏将偏移值添加到地址，并将生成的地址强制转换为指定的类型。
keywords:
- WDF_PTR_ADD_OFFSET_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8088e7b0af73592d2624fe8e7390a9c868efb824
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839183"
---
# <a name="wdf_ptr_add_offset_type-macro"></a>WDF_PTR_ADD_OFFSET_TYPE 宏


**WDF_PTR_ADD_OFFSET_TYPE** 宏将偏移值添加到地址，并将生成的地址强制转换为指定的类型。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
_type WDF_PTR_ADD_OFFSET_TYPE(
    _ptr,
    _offset,
    _type
);
```

<a name="parameters"></a>参数
----------

*_ptr*   
指定地址。

*_offset*   
指定偏移量值（以字节为单位）。

*_type*   
指定要返回的数据类型。

<a name="return-value"></a>返回值
------------

返回一个指向生成的地址的指针。 在宏的 *_type* 参数中选择返回值的数据类型。

<a name="remarks"></a>备注
-------

宏的定义如下：

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
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.5</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfcore (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

 

 






