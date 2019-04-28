---
title: IPrinterBidiSchemaResponses AddEnum 方法
description: AddEnum 方法将添加新的响应的类型 BIDI\_到集合的枚举。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: B172DF90-63F8-4064-8781-EB0E8D799C1A
keywords:
- AddEnum 方法打印设备
- AddEnum 方法打印设备，IPrinterBidiSchemaResponses 接口
- IPrinterBidiSchemaResponses 接口打印设备，AddEnum 方法
topic_type:
- apiref
api_name:
- IPrinterBidiSchemaResponses.AddEnum
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4cd1e0bd3633f61d6bfdd8b0ec647e6916d79bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351643"
---
# <a name="iprinterbidischemaresponsesaddenum-method"></a>IPrinterBidiSchemaResponses::AddEnum 方法

AddEnum 方法将添加新的响应的类型 BIDI\_到集合的枚举。

<a name="syntax"></a>语法
------

```cpp
HRESULT AddEnum(
  [in] BSTR bstrSchema,
  [in] BSTR bstrValue
);
```

<a name="parameters"></a>Parameters
----------

*bstrSchema* \[in\]  
架构。

*bstrValue* \[in\]  
类型的枚举值。

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
