---
title: IPrinterBidiSchemaResponses AddInt32 方法
description: AddInt32 方法将添加新的响应的类型 BIDI\_INT 到集合。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: F937B098-9C13-4337-82A6-C26DAA8B7068
keywords:
- AddInt32 方法打印设备
- AddInt32 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddInt32 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddInt32
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c980d99dc50e5da1e731132b5ffe7d9703267cc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351679"
---
# <a name="iprinterbidischemaresponsesaddint32-method"></a>IPrinterBidiSchemaResponses::AddInt32 方法

AddInt32 方法将添加新的响应的类型 BIDI\_INT 到集合。

<a name="syntax"></a>语法
------

```cpp
HRESULT  AddInt32(
  [in] BSTR bstrSchema,
  [in] LONG lValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*lValue* \[in\]  
新值。

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
