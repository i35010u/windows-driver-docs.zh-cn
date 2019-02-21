---
title: IPrinterBidiSchemaResponses AddNull 方法
description: AddNull 方法将添加新的响应的类型 BIDI\_集合为 NULL。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 36796227-7EE4-43C8-9AD7-51A3929D1CE2
keywords:
- AddNull 方法打印设备
- AddNull 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddNull 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddNull
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21dcc47f9497003d4b79d1f2f21398a65a55fe21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532995"
---
# <a name="iprinterbidischemaresponsesaddnull-method"></a>IPrinterBidiSchemaResponses::AddNull 方法

AddNull 方法将添加新的响应的类型 BIDI\_集合为 NULL。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddNull(
  [in] BSTR bstrSchema
);
```

<a name="parameters"></a>参数
----------

*bstrSchema* \[in\]  
架构名称。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

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
<td>桌面设备</td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
