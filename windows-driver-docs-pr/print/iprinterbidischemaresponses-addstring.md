---
title: IPrinterBidiSchemaResponses AddString 方法
description: AddString 方法将添加新的响应的类型 BIDI\_到集合的字符串。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ACBE70E7-5A2B-4472-B1A3-40722D849119
keywords:
- AddString 方法打印设备
- AddString 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddString 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddString
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 843f04bb47bcc68603f8be4bbecdb8cd58c4bbdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351666"
---
# <a name="iprinterbidischemaresponsesaddstring-method"></a>IPrinterBidiSchemaResponses::AddString 方法

AddString 方法将添加新的响应的类型 BIDI\_到集合的字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddString(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*bstrValue* \[in\]  
字符串响应中。

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
