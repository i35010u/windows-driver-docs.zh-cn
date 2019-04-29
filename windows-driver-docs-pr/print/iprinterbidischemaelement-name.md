---
title: IPrinterBidiSchemaElement 名称方法
description: 该名称方法返回 Bidi 架构元素名称。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 682B3DFE-EE21-4C96-B585-1D63287C33A0
keywords:
- 名称方法打印设备
- 命名方法打印设备 IPrinterBidiSchemaElement 接口
- IPrinterBidiSchemaElement 接口打印设备，名称方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaElement.Name
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbe247e5f9cd7f9716a4bfa7c401b6a6d1bbc18c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324827"
---
# <a name="iprinterbidischemaelementname-method"></a>IPrinterBidiSchemaElement::Name 方法

该名称方法返回 Bidi 架构元素名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT Name(
  [out, retval] BSTR *pbstrSchema
);
```

<a name="parameters"></a>Parameters
----------

*pbstrSchema* \[out, retval\]  
返回的元素名称。

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

[**IPrinterBidiSchemaElement**](iprinterbidischemaelement-interface.md)
