---
title: IPrinterBidiSchemaResponses AddFloat 方法
description: AddFloat 方法将双向 FLOAT 类型的新响应添加 \_ 到集合中。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- AddFloat 方法打印设备
- AddFloat 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddFloat 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddFloat
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbb494a27e8b704bddc374245d170c0c20f32ac0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835575"
---
# <a name="iprinterbidischemaresponsesaddfloat-method"></a>IPrinterBidiSchemaResponses：： AddFloat 方法

AddFloat 方法将双向 FLOAT 类型的新响应添加 \_ 到集合中。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddFloat(
  [in] BSTR    bstrSchema,
  [in] FLOAT  fValue 
);
```

<a name="parameters"></a>参数
----------

 *bstrSchema* \[中\]  
架构。

 *fValue* \[中\]  
新的浮点值。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

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
<td>台式机</td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
