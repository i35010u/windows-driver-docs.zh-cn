---
title: WDF_PTR_GET_OFFSET 宏
description: WDF_PTR_GET_OFFSET 宏中减去另一个地址中的地址，并返回结果的偏移量的值。
ms.assetid: b5159207-ba5c-4924-a06e-725ccd3c8a12
keywords:
- WDF_PTR_GET_OFFSET 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1782a7545ace74a23948ebd19b7bad579b04542
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544199"
---
# <a name="wdfptrgetoffset-macro"></a>WDF_PTR_GET_OFFSET 宏


**WDF_PTR_GET_OFFSET**宏中减去另一个地址中的地址，并返回结果的偏移量的值。

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
指定要从起始地址中减去的值。

*_addr*   
指定的起始地址。

<a name="return-value"></a>返回值
------------

返回两个指定的地址之间的偏移量。

<a name="remarks"></a>备注
-------

定义宏，如下所示：

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
<td><p>标头</p></td>
<td>Wdfcore.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

 

 






