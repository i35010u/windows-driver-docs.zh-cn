---
title: IPrinterBidiSchemaResponses AddBool 方法
description: AddBool 方法将添加新的响应的类型 BIDI\_到集合的布尔值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 8D1C9198-DE72-4348-84EE-C3B875D14E6A
keywords:
- AddBool 方法打印设备
- AddBool 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddBool 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddBool
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e091d231c1bda1bc98f6260b26e073dd03f1f1ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351688"
---
# <a name="iprinterbidischemaresponsesaddbool-method"></a>IPrinterBidiSchemaResponses::AddBool 方法

AddBool 方法将添加新的响应的类型 BIDI\_到集合的布尔值。

<a name="syntax"></a>语法
------

```cpp
HRESULT  AddBool(
  [in] BSTR bstrSchema,
  [in] BOOL bValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*bValue* \[in\]  
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
