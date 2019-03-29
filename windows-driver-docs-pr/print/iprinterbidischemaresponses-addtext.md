---
title: IPrinterBidiSchemaResponses AddText 方法
description: AddText 方法将添加新的响应的类型 BIDI\_到集合的文本。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 2421D77A-E0B2-4114-A27E-59E0D9A88E7C
keywords:
- AddText 方法打印设备
- AddText 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddText 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddText
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c35fca3151be6c17859aacecacbb900173c7fae1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564997"
---
# <a name="iprinterbidischemaresponsesaddtext-method"></a>IPrinterBidiSchemaResponses::AddText 方法

AddText 方法将添加新的响应的类型 BIDI\_到集合的文本。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddText(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*bstrValue* \[in\]  
文本。

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
<td><p>Windows 8 及更高版本</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterBidiSchemaResponses**](iprinterbidischemaresponses.md)
