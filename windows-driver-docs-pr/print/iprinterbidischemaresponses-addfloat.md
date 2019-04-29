---
title: IPrinterBidiSchemaResponses AddFloat 方法
description: AddFloat 方法将添加新的响应的类型 BIDI\_浮动到集合。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 99A66884-3528-43C3-AC56-CE0AA64AB328
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
ms.openlocfilehash: e60dffed4a7b0147fd7e8266d987f8e147db8af9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373383"
---
# <a name="iprinterbidischemaresponsesaddfloat-method"></a>IPrinterBidiSchemaResponses::AddFloat 方法

AddFloat 方法将添加新的响应的类型 BIDI\_浮动到集合。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddFloat(
  [in] BSTR    bstrSchema,
  [in] FLOAT  fValue 
);
```

<a name="parameters"></a>Parameters
----------

 *bstrSchema* \[in\]  
架构。

 *fValue* \[in\]  
新的浮动点值。

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
<td><p>Version</p></td>
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
