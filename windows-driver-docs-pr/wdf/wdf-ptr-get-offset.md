---
title: WDF_PTR_GET_OFFSET 宏
description: WDF_PTR_GET_OFFSET 宏从另一个地址减去一个地址，并返回生成的偏移量值。
keywords:
- WDF_PTR_GET_OFFSET 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bde3d1f24310d1d71ae7f4fe06937d03deef430
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809779"
---
# <a name="wdf_ptr_get_offset-macro"></a>WDF_PTR_GET_OFFSET 宏


**WDF_PTR_GET_OFFSET** 宏从另一个地址减去一个地址，并返回生成的偏移量值。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
size_t WDF_PTR_GET_OFFSET(
    _base,
    _addr
);
```

<a name="parameters"></a>参数
----------

*_base*   
指定要从起始地址减去的值。

*_addr*   
指定起始地址。

<a name="return-value"></a>返回值
------------

返回两个指定地址之间的偏移量。

<a name="remarks"></a>备注
-------

宏的定义如下：

```ManagedCPlusPlus
#define WDF_PTR_GET_OFFSET(_base, _addr) \
        (size_t) (((PUCHAR) _addr) - ((PUCHAR) _base))
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

 

 






